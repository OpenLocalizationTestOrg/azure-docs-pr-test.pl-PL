---
title: "Jak delegować subskrypcji użytkownika rejestracji i produktu"
description: "Dowiedz się, jak delegować rejestracji i produktu subskrypcji użytkownika do innej firmy w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="fc3d0-103">Jak delegować subskrypcji użytkownika rejestracji i produktu</span><span class="sxs-lookup"><span data-stu-id="fc3d0-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="fc3d0-104">Delegowanie umożliwia przy użyciu istniejącej witryny sieci Web do obsługi projektanta logowania — w/tworzenia konta i subskrypcji do produktów, a nie za pomocą wbudowanej funkcji w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="fc3d0-105">Dzięki temu witryny sieci Web do własnych danych użytkownika i przeprowadzania weryfikacji tych kroków w niestandardowy sposób.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="fc3d0-106"><a name="delegate-signin-up"></a>Developer delegowanie logowania i rejestrowania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="fc3d0-107">Delegować developer logowania i rejestrowania do istniejącej witryny sieci Web należy utworzyć delegowanie specjalne punkt końcowy w swojej witrynie, który działa jako punkt wejścia dla takiego żądania inicjowanych z poziomu portalu dla deweloperów zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="fc3d0-108">Końcowe przepływ pracy będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="fc3d0-109">Deweloper kliknięć łącze logowania lub tworzenia konta w portalu dla deweloperów zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="fc3d0-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="fc3d0-110">Przeglądarka jest przekierowywany do punktu końcowego delegowania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="fc3d0-111">Punkt końcowy delegowania w zamian przekierowuje do lub przedstawia prośba użytkownika logowania lub zapisywania do interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fc3d0-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="fc3d0-112">W przypadku powodzenia zostanie przekierowany użytkownik w wróć do strony portalu deweloperów zarządzanie interfejsami API uruchomienia z</span><span class="sxs-lookup"><span data-stu-id="fc3d0-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="fc3d0-113">Aby rozpocząć, umożliwia pierwszy zarządzanie interfejsami API konfiguracji do rozsyłania żądań za pośrednictwem punktu końcowego delegowania.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="fc3d0-114">W portalu wydawcy interfejsu API zarządzania kliknij polecenie **zabezpieczeń** , a następnie kliknij przycisk **delegowania** kartę.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="fc3d0-115">Kliknij pole wyboru, aby włączyć "Delegate logowania & rejestracji".</span><span class="sxs-lookup"><span data-stu-id="fc3d0-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Strony delegowania][api-management-delegation-signin-up]

* <span data-ttu-id="fc3d0-117">Zdecyduj, co adres URL punktu końcowego specjalne delegowania zostanie i wprowadź go w **adres URL punktu końcowego delegowania** pola.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="fc3d0-118">W ramach **klucz uwierzytelniania delegowania** pola wprowadź klucz tajny, który będzie używany do obliczenia podpisu dostarczone do weryfikacji upewnić się, czy żądanie jest rzeczywiście pochodzi z usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="fc3d0-119">Możesz kliknąć **Generowanie** przycisk, aby mieć interfejsu API zarządzania losowego generowania klucza.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="fc3d0-120">Teraz musisz utworzyć **punktu końcowego delegowania**.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="fc3d0-121">Musi przeprowadzić szereg akcji:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="fc3d0-122">Otrzyma żądanie w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="fc3d0-123">*http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {adres URL strony źródła} & soli = {ciąg} & sig = {ciąg}*</span><span class="sxs-lookup"><span data-stu-id="fc3d0-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="fc3d0-124">Parametry zapytania w przypadku logowania / tworzenia konta:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="fc3d0-125">**Operacja**: Określa jaki typ żądania delegowania jest — może być tylko **SignIn** w takim przypadku</span><span class="sxs-lookup"><span data-stu-id="fc3d0-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="fc3d0-126">**returnUrl**: adres URL strony, gdy użytkownik kliknął Link logowania lub zapisywania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="fc3d0-127">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="fc3d0-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="fc3d0-128">**SIG**: skrót obliczona zabezpieczeń do użycia w porównaniu do własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="fc3d0-129">Sprawdź, czy żądanie jest pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="fc3d0-130">Obliczeniowe skrótu HMAC SHA512 ciągu na podstawie **returnUrl** i **soli** parametry zapytania ([przykładowy kod podany poniżej]):</span><span class="sxs-lookup"><span data-stu-id="fc3d0-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="fc3d0-131">Metoda HMAC (**soli** + "\n" + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="fc3d0-132">Porównanie obliczonego powyżej skrót z wartością **sig** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="fc3d0-133">Jeśli dwa skróty są zgodne, przejdź do następnego kroku, odrzuciła żądanie, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="fc3d0-134">Sprawdź, czy otrzymują żądanie logowania w/logowania — w górę: **operacji** parametru zapytania zostanie ustawiony na "**rejestrowanie**".</span><span class="sxs-lookup"><span data-stu-id="fc3d0-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="fc3d0-135">Interfejs użytkownika do logowania lub zapisywania do zaoferowania użytkownikowi</span><span class="sxs-lookup"><span data-stu-id="fc3d0-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="fc3d0-136">Jeśli użytkownik jest zarejestrowanie się należy utworzyć odpowiednie konta dla nich w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="fc3d0-137">[Utwórz użytkownika] przy użyciu interfejsu API REST zarządzania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="fc3d0-138">Po tej czynności upewnij się, Ustaw identyfikator użytkownika, takie same, który znajduje się w magazynie użytkownika lub identyfikator, który użytkownik może przechowywać ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="fc3d0-139">Po pomyślnym uwierzytelnieniu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="fc3d0-140">[żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on] za pośrednictwem interfejsu API REST zarządzania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fc3d0-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="fc3d0-141">Dołącz returnUrl parametru zapytania do adresu URL logowania jednokrotnego otrzymane od wywołania interfejsu API powyżej:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="fc3d0-142">https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url np.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="fc3d0-143">przekierowuje użytkownika do utworzonych powyższy adres URL</span><span class="sxs-lookup"><span data-stu-id="fc3d0-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="fc3d0-144">Oprócz **SignIn** operacji, można również wykonywać Zarządzanie kontami przez wykonanie poprzednich kroków i przy użyciu jednej z następujących czynności.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="fc3d0-145">**Element ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="fc3d0-145">**ChangePassword**</span></span>
* <span data-ttu-id="fc3d0-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="fc3d0-146">**ChangeProfile**</span></span>
* <span data-ttu-id="fc3d0-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="fc3d0-147">**CloseAccount**</span></span>

<span data-ttu-id="fc3d0-148">Należy podać następujące parametry zapytania dla operacji zarządzania kontem.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="fc3d0-149">**Operacja**: Określa typ żądania delegowania jest (Element ChangePassword, ChangeProfile lub CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="fc3d0-150">**Identyfikator userId**: identyfikator użytkownika konta do zarządzania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="fc3d0-151">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="fc3d0-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="fc3d0-152">**SIG**: skrót obliczona zabezpieczeń do użycia w porównaniu do własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="fc3d0-153"><a name="delegate-product-subscription"></a>Delegowanie subskrypcji produktu</span><span class="sxs-lookup"><span data-stu-id="fc3d0-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="fc3d0-154">Delegowanie subskrypcji produktu działa podobnie do delegowania użytkownika logowania/w górę.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="fc3d0-155">Końcowe przepływu pracy, należy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="fc3d0-156">Deweloper wybiera produktu w portalu dla deweloperów usługi API Management i kliknie przycisk Subskrybuj</span><span class="sxs-lookup"><span data-stu-id="fc3d0-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="fc3d0-157">Przeglądarka jest przekierowywany do punktu końcowego delegowania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="fc3d0-158">Punkt końcowy delegowania wykonuje kroki subskrypcji produktu wymagane — to zależy od użytkownika i może spowodować przekierowanie do innej strony do żądania informacji dotyczących rozliczeń, prosząc dodatkowych pytań lub po prostu przechowywanie informacji i nie wymaga żadnych działań użytkownika</span><span class="sxs-lookup"><span data-stu-id="fc3d0-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="fc3d0-159">Aby włączyć funkcję, na **delegowania** kliknij **delegować subskrypcji produktu**.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="fc3d0-160">Następnie upewnij się, że punkt końcowy delegowania wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="fc3d0-161">Otrzyma żądanie w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="fc3d0-162">*{Operacja} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {produktu do subskrybowania} & userId = {użytkownika zgłaszającego żądanie} & ziarna = {ciąg} & sig = {ciąg}*</span><span class="sxs-lookup"><span data-stu-id="fc3d0-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="fc3d0-163">Parametry zapytania w przypadku subskrypcji produktu:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="fc3d0-164">**Operacja**: Określa, jakiego typu żądanie delegowania jest.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="fc3d0-165">Dla subskrypcji produktu żądania prawidłowe opcje to:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="fc3d0-166">"Subskrypcji": żądanie do subskrybowania użytkownika do danego produktu z podany identyfikator (patrz poniżej)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="fc3d0-167">"Anuluj subskrypcję": żądanie anulowania subskrypcji użytkownika z produktu</span><span class="sxs-lookup"><span data-stu-id="fc3d0-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="fc3d0-168">"Odnowić": requst odnowienia subskrypcji (np. może być wygasa)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="fc3d0-169">**productId**: identyfikator produktu użytkownik zażądał do subskrybowania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="fc3d0-170">**Identyfikator userId**: identyfikator użytkownika, dla którego żądań</span><span class="sxs-lookup"><span data-stu-id="fc3d0-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="fc3d0-171">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="fc3d0-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="fc3d0-172">**SIG**: skrót obliczona zabezpieczeń do użycia w porównaniu do własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="fc3d0-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="fc3d0-173">Sprawdź, czy żądanie jest pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="fc3d0-174">Obliczeniowe SHA512 HMAC ciągu na podstawie **productId**, **userId** i **soli** parametry zapytania:</span><span class="sxs-lookup"><span data-stu-id="fc3d0-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="fc3d0-175">Metoda HMAC (**soli** + "\n" + **productId** + "\n" + **userId**)</span><span class="sxs-lookup"><span data-stu-id="fc3d0-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="fc3d0-176">Porównanie obliczonego powyżej skrót z wartością **sig** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="fc3d0-177">Jeśli dwa skróty są zgodne, przejdź do następnego kroku, odrzuciła żądanie, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="fc3d0-178">Przetwarzania żadnych subskrypcji produktów na podstawie typu żądanej w operacji **operacji** -np. rozliczeń, dalsze pytania itp.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="fc3d0-179">W subskrypcji pomyślnie użytkownikowi produktu na Twojej stronie, subskrypcja użytkownikowi produktu interfejsu API zarządzania przez [wywołanie interfejsu API REST dla subskrypcji produktu].</span><span class="sxs-lookup"><span data-stu-id="fc3d0-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="fc3d0-180"><a name="delegate-example-code"></a> Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="fc3d0-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="fc3d0-181">Te przykłady pokazują, jak wykonać *klucz sprawdzania poprawności delegowania*, znajduje w ekranie delegowania portalu wydawcy, można utworzyć HMAC, który jest następnie używany do sprawdzania poprawności podpisu, potwierdzania ważności returnUrl przekazany .</span><span class="sxs-lookup"><span data-stu-id="fc3d0-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="fc3d0-182">Ten sam kod działa w przypadku productId i userId nieznaczne modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="fc3d0-183">**Kod C# do generowania skrótu returnUrl**</span><span class="sxs-lookup"><span data-stu-id="fc3d0-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="fc3d0-184">**Umożliwia generowanie skrótów returnUrl kodu NodeJS**</span><span class="sxs-lookup"><span data-stu-id="fc3d0-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="fc3d0-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc3d0-185">Next steps</span></span>
<span data-ttu-id="fc3d0-186">Aby uzyskać więcej informacji na delegowania zobacz poniższe wideo.</span><span class="sxs-lookup"><span data-stu-id="fc3d0-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="fc3d0-187">[żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="fc3d0-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="fc3d0-188">[Utwórz użytkownika]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="fc3d0-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="fc3d0-189">[wywołanie interfejsu API REST dla subskrypcji produktu]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="fc3d0-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="fc3d0-190">[przykładowy kod podany poniżej]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="fc3d0-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
