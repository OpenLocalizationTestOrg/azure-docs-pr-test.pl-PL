---
title: "Formanty strony Zarządzanie interfejsami API aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat formantów strony hello dostępne do użycia w szablonach portalu deweloperów w usłudze Azure API Management."
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="15385-103">Formanty strony Zarządzanie interfejsami API Azure</span><span class="sxs-lookup"><span data-stu-id="15385-103">Azure API Management page controls</span></span>
<span data-ttu-id="15385-104">Zarządzanie interfejsami API Azure udostępnia powitania po formanty do użycia w szablonach portalu deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="15385-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="15385-105">toouse formantu, umieścić go w lokalizacji hello żądanego szablonu portalu deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="15385-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="15385-106">Niektóre formanty, takie jak hello [akcje aplikacji](#app-actions) kontrolować, ma parametry, jak przedstawiono na powitania poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="15385-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="15385-107">Witaj wartości parametrów hello są przekazywane w jako część modelu danych hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="15385-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="15385-108">W większości przypadków, możesz po prostu wkleić hello podać przykład dla każdego formantu dla niego toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="15385-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="15385-109">Aby uzyskać więcej informacji na wartości parametrów hello widać hello sekcji modelu danych do każdego szablonu, w którym można użyć formantu.</span><span class="sxs-lookup"><span data-stu-id="15385-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="15385-110">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="15385-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="15385-111">Formantów strony szablonu portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="15385-112">Akcje aplikacji</span><span class="sxs-lookup"><span data-stu-id="15385-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="15385-113">Rejestrowanie Basic</span><span class="sxs-lookup"><span data-stu-id="15385-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="15385-114">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="15385-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="15385-115">dostawców</span><span class="sxs-lookup"><span data-stu-id="15385-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="15385-116">formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="15385-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="15385-117">rejestracji</span><span class="sxs-lookup"><span data-stu-id="15385-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="15385-118">przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15385-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="15385-119">Anuluj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="15385-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="15385-120"><a name="app-actions"></a>Akcje aplikacji</span><span class="sxs-lookup"><span data-stu-id="15385-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="15385-121">Witaj `app-actions` kontroli udostępnia interfejs użytkownika do interakcji z aplikacjami na powitania strony profilu użytkownika w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="15385-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="15385-122">![& #45 aplikacji; kontrolka akcje](./media/api-management-page-controls/APIM-app-actions-control.png "APIM kontroli akcje aplikacji")</span><span class="sxs-lookup"><span data-stu-id="15385-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-123">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-124">Parameters</span></span>  
  
|<span data-ttu-id="15385-125">Parametr</span><span class="sxs-lookup"><span data-stu-id="15385-125">Parameter</span></span>|<span data-ttu-id="15385-126">Opis</span><span class="sxs-lookup"><span data-stu-id="15385-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="15385-127">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="15385-127">appId</span></span>|<span data-ttu-id="15385-128">Identyfikator Hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="15385-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-129">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-129">Developer portal templates</span></span>  
 <span data-ttu-id="15385-130">Witaj `app-actions` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-131">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="15385-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="15385-132"><a name="basic-signin"></a>Rejestrowanie Basic</span><span class="sxs-lookup"><span data-stu-id="15385-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="15385-133">Witaj `basic-signin` kontroli udostępnia kontrolkę do zbierania informacji w hello logowania użytkownika Zaloguj się na stronie w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="15385-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="15385-134">![Basic &#45; kontrolka signin](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic Rejestrowanie formantu")</span><span class="sxs-lookup"><span data-stu-id="15385-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-135">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-136">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-136">Parameters</span></span>  
 <span data-ttu-id="15385-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-138">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-138">Developer portal templates</span></span>  
 <span data-ttu-id="15385-139">Witaj `basic-signin` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-140">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="15385-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="15385-141"><a name="paging-control"></a>Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="15385-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="15385-142">Witaj `paging-control` zawiera funkcje stronicowania po developer portal stron, które wyświetlania listy elementów.</span><span class="sxs-lookup"><span data-stu-id="15385-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="15385-143">![stronicowanie kontroli](./media/api-management-page-controls/APIM-paging-control.png "APIM formant stronicowania")</span><span class="sxs-lookup"><span data-stu-id="15385-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-144">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-145">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-145">Parameters</span></span>  
 <span data-ttu-id="15385-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-147">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-147">Developer portal templates</span></span>  
 <span data-ttu-id="15385-148">Witaj `paging-control` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-149">Lista interfejsu API</span><span class="sxs-lookup"><span data-stu-id="15385-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="15385-150">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="15385-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="15385-151">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="15385-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="15385-152"><a name="providers"></a>dostawców</span><span class="sxs-lookup"><span data-stu-id="15385-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="15385-153">Witaj `providers` kontroli udostępnia kontrolkę wyboru dostawcy uwierzytelniania w hello stronę w portalu dla deweloperów hello logowania.</span><span class="sxs-lookup"><span data-stu-id="15385-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="15385-154">![Formant dostawców](./media/api-management-page-controls/APIM-providers-control.png "APIM dostawców kontroli")</span><span class="sxs-lookup"><span data-stu-id="15385-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-155">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-156">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-156">Parameters</span></span>  
 <span data-ttu-id="15385-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-158">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-158">Developer portal templates</span></span>  
 <span data-ttu-id="15385-159">Witaj `providers` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-160">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="15385-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="15385-161"><a name="search-control"></a>formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="15385-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="15385-162">Witaj `search-control` udostępnia funkcje wyszukiwania na deweloperów na stronach portalu zawierające listę elementów.</span><span class="sxs-lookup"><span data-stu-id="15385-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="15385-163">![Wyszukaj kontroli](./media/api-management-page-controls/APIM-search-control.png "APIM formant wyszukiwania")</span><span class="sxs-lookup"><span data-stu-id="15385-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-164">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-165">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-165">Parameters</span></span>  
 <span data-ttu-id="15385-166">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-167">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-167">Developer portal templates</span></span>  
 <span data-ttu-id="15385-168">Witaj `search-control` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-169">Lista interfejsu API</span><span class="sxs-lookup"><span data-stu-id="15385-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="15385-170">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="15385-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="15385-171"><a name="sign-up"></a>rejestracji</span><span class="sxs-lookup"><span data-stu-id="15385-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="15385-172">Witaj `sign-up` kontroli udostępnia kontrolkę do zbierania informacji o profilu użytkownika w stronę w portalu dla deweloperów hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="15385-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="15385-173">![znak &#45; w górę kontrolki](./media/api-management-page-controls/APIM-sign-up-control.png "APIM zapisywania kontrolki")</span><span class="sxs-lookup"><span data-stu-id="15385-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-174">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-175">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-175">Parameters</span></span>  
 <span data-ttu-id="15385-176">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-177">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-177">Developer portal templates</span></span>  
 <span data-ttu-id="15385-178">Witaj `sign-up` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-179">Zarejestruj się</span><span class="sxs-lookup"><span data-stu-id="15385-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="15385-180"><a name="subscribe-button"></a>przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15385-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="15385-181">Witaj `subscribe-button` udostępnia kontrolkę do subskrypcji produktu tooa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15385-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="15385-182">![Subskrypcja &#45; button — formant](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM formantu przycisku subskrypcji")</span><span class="sxs-lookup"><span data-stu-id="15385-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-183">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-184">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-184">Parameters</span></span>  
 <span data-ttu-id="15385-185">Brak.</span><span class="sxs-lookup"><span data-stu-id="15385-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-186">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-186">Developer portal templates</span></span>  
 <span data-ttu-id="15385-187">Witaj `subscribe-button` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-188">Produktu</span><span class="sxs-lookup"><span data-stu-id="15385-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="15385-189"><a name="subscription-cancel"></a>Anuluj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="15385-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="15385-190">Witaj `subscription-cancel` kontroli udostępnia kontrolkę do anulowania subskrypcji produktu tooa hello strony profilu użytkownika w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="15385-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="15385-191">![Subskrypcja &#45; Anuluj kontroli](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM kontroli Anuluj subskrypcję")</span><span class="sxs-lookup"><span data-stu-id="15385-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="15385-192">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="15385-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="15385-193">Parametry</span><span class="sxs-lookup"><span data-stu-id="15385-193">Parameters</span></span>  
  
|<span data-ttu-id="15385-194">Parametr</span><span class="sxs-lookup"><span data-stu-id="15385-194">Parameter</span></span>|<span data-ttu-id="15385-195">Opis</span><span class="sxs-lookup"><span data-stu-id="15385-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="15385-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="15385-196">subscriptionId</span></span>|<span data-ttu-id="15385-197">Identyfikator Hello hello toocancel subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15385-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="15385-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="15385-198">cancelUrl</span></span>|<span data-ttu-id="15385-199">Subskrypcja Hello anulować adresu URL.</span><span class="sxs-lookup"><span data-stu-id="15385-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="15385-200">Szablony portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="15385-200">Developer portal templates</span></span>  
 <span data-ttu-id="15385-201">Witaj `subscription-cancel` kontroli mogą być używane w hello następujące szablony portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="15385-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="15385-202">Produktu</span><span class="sxs-lookup"><span data-stu-id="15385-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="15385-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15385-203">Next steps</span></span>
<span data-ttu-id="15385-204">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="15385-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
