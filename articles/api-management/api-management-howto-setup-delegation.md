---
title: "aaaHow toodelegate użytkownika rejestracji i produktu subskrypcji"
description: "Dowiedz się, jak toodelegate użytkownika rejestracji i produktu subskrypcji tooa innej firmy w usłudze Azure API Management."
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="5d7cb-103">Jak toodelegate użytkownika rejestracji i produktu subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5d7cb-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="5d7cb-104">Delegowanie pozwala toouse istniejącej witryny sieci Web do obsługi tooproducts logowania — w/tworzenia konta i subskrypcji dewelopera jako przeciwieństwie toousing hello wbudowanej funkcji w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="5d7cb-105">To umożliwia dane użytkowników hello tooown witryny sieci Web i sprawdzania poprawności hello tych kroków w niestandardowy sposób.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="5d7cb-106"><a name="delegate-signin-up"></a>Developer delegowanie logowania i rejestrowania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="5d7cb-107">toodelegate developer tooyour logowania i rejestrowania istniejącej witryny sieci Web w swojej witrynie, który działa jako punkt wejścia dla takiego żądania inicjowanych z poziomu portalu dla deweloperów usługi API Management hello hello konieczne będzie toocreate punktu końcowego specjalne delegowania.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="5d7cb-108">Hello końcowego przepływ pracy będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="5d7cb-109">Deweloper kliknie łącze logowania lub zapisywania hello na powitania portalu dla deweloperów zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="5d7cb-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="5d7cb-110">Przeglądarka jest punkt końcowy delegowania toohello przekierowane</span><span class="sxs-lookup"><span data-stu-id="5d7cb-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="5d7cb-111">Punkt końcowy delegowania w zamian przekierowuje tooor przedstawia interfejsu użytkownika pytaniem, czy użytkownik toosign w lub zapisywania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="5d7cb-112">W przypadku powodzenia hello użytkownik jest przekierowane toohello wstecz zarządzanie interfejsami API developer strony portalu uruchomienia z</span><span class="sxs-lookup"><span data-stu-id="5d7cb-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="5d7cb-113">toobegin, umożliwia pierwszy Konfiguracja interfejsu API zarządzania tooroute żądań za pośrednictwem punktu końcowego delegowania.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="5d7cb-114">W portalu wydawcy zarządzanie interfejsami API hello, kliknij polecenie **zabezpieczeń** , a następnie kliknij przycisk hello **delegowania** kartę. Kliknij przycisk tooenable wyboru hello "Delegate logowania & rejestracji".</span><span class="sxs-lookup"><span data-stu-id="5d7cb-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Strony delegowania][api-management-delegation-signin-up]

* <span data-ttu-id="5d7cb-116">Zdecyduj, co hello adres URL punktu końcowego specjalne delegowania zostanie i wprowadź go w hello **adres URL punktu końcowego delegowania** pola.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="5d7cb-117">W ramach hello **klucz uwierzytelniania delegowania** polu Wprowadź hasło, które będzie używane toocompute tooyou podpisu podane dla tooensure weryfikacji, który hello żądania jest rzeczywiście pochodzi z usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="5d7cb-118">Możesz kliknąć hello **Generowanie** toohave przycisk interfejsu API zarządzania losowego generowania klucza dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="5d7cb-119">Teraz należy toocreate hello **punktu końcowego delegowania**.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="5d7cb-120">Tooperform ma wiele akcji:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="5d7cb-121">Otrzyma żądanie w hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="5d7cb-122">*http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {adres URL strony źródła} & soli = {ciąg} & sig = {ciąg}*</span><span class="sxs-lookup"><span data-stu-id="5d7cb-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="5d7cb-123">Parametry zapytania w przypadku logowania / tworzenia konta hello:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="5d7cb-124">**Operacja**: Określa jaki typ żądania delegowania jest — może być tylko **SignIn** w takim przypadku</span><span class="sxs-lookup"><span data-stu-id="5d7cb-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="5d7cb-125">**returnUrl**: hello adres URL strony hello gdzie hello użytkownik kliknął link logowania lub zapisywania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="5d7cb-126">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5d7cb-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="5d7cb-127">**SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="5d7cb-128">Sprawdź, czy Żądanie hello pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="5d7cb-129">Obliczeniowe skrótu HMAC SHA512 ciągu oparte na powitania **returnUrl** i **soli** parametry zapytania ([przykładowy kod podany poniżej]):</span><span class="sxs-lookup"><span data-stu-id="5d7cb-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="5d7cb-130">Metoda HMAC (**soli** + "\n" + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="5d7cb-131">Porównaj wartości toohello obliczonego powyżej skrótu hello hello **sig** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="5d7cb-132">Jeśli skróty dwóch hello są zgodne, przesuń w następnym kroku toohello, w przeciwnym razie odmowy żądania hello.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="5d7cb-133">Sprawdź, czy otrzymują żądanie logowania w/logowania — w górę: hello **operacji** parametru zapytania zostanie ustawiona zbyt "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="5d7cb-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="5d7cb-134">Obecny użytkownik hello przy użyciu interfejsu użytkownika w toosign lub zapisywania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="5d7cb-135">Jeśli użytkownik hello jest zarejestrowanie się masz toocreate odpowiadającego mu konta dla nich w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="5d7cb-136">[Utwórz użytkownika] z hello interfejsu API REST zarządzania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="5d7cb-137">Po tej czynności upewnij się, ustaw toohello identyfikator użytkownika hello, takie same, który znajduje się w magazynie użytkownika lub identyfikator tooan, który użytkownik może przechowywać ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="5d7cb-138">Gdy hello pomyślnego uwierzytelnienia użytkownika:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="5d7cb-139">[żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on] za pośrednictwem hello interfejsu API REST zarządzania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5d7cb-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="5d7cb-140">Dołącz returnUrl toohello parametru zapytania URL logowania jednokrotnego otrzymany z powyższego wywołania hello interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="5d7cb-141">https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url np.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="5d7cb-142">adres URL utworzony przekierowania hello użytkownika toohello powyżej</span><span class="sxs-lookup"><span data-stu-id="5d7cb-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="5d7cb-143">W dodatku toohello **SignIn** operacji, można również wykonywać Zarządzanie kontami po poprzednich kroków hello i przy użyciu jednej z hello następujące operacje.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="5d7cb-144">**Element ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="5d7cb-144">**ChangePassword**</span></span>
* <span data-ttu-id="5d7cb-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="5d7cb-145">**ChangeProfile**</span></span>
* <span data-ttu-id="5d7cb-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="5d7cb-146">**CloseAccount**</span></span>

<span data-ttu-id="5d7cb-147">Należy podać następujące parametry zapytania dla operacji zarządzania kontem hello.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="5d7cb-148">**Operacja**: Określa typ żądania delegowania jest (Element ChangePassword, ChangeProfile lub CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="5d7cb-149">**Identyfikator userId**: identyfikator użytkownika hello hello toomanage konta</span><span class="sxs-lookup"><span data-stu-id="5d7cb-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="5d7cb-150">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5d7cb-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="5d7cb-151">**SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="5d7cb-152"><a name="delegate-product-subscription"></a>Delegowanie subskrypcji produktu</span><span class="sxs-lookup"><span data-stu-id="5d7cb-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="5d7cb-153">Delegowanie subskrypcji produktu działa podobnie toodelegating użytkownika logowania/w górę.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="5d7cb-154">Witaj końcowego przepływu pracy, należy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="5d7cb-155">Deweloper wybiera produktu w portalu dla deweloperów usługi API Management hello i kliknie przycisk Subskrybuj hello</span><span class="sxs-lookup"><span data-stu-id="5d7cb-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="5d7cb-156">Przeglądarka jest punkt końcowy delegowania toohello przekierowane</span><span class="sxs-lookup"><span data-stu-id="5d7cb-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="5d7cb-157">Punkt końcowy delegowania wykonuje kroki subskrypcji produktu wymagane — to jest uruchomiony tooyou i może pociągać za sobą przekierowania toorequest strony tooanother informacji dotyczących rozliczeń, prosząc dodatkowych pytań lub hello informacje są przechowywane po prostu i nie wymaga żadnych działań użytkownika</span><span class="sxs-lookup"><span data-stu-id="5d7cb-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="5d7cb-158">Funkcje hello tooenable, na powitania **delegowania** kliknij **delegować subskrypcji produktu**.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="5d7cb-159">Następnie upewnij się, że punkt końcowy delegowania hello wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="5d7cb-160">Otrzyma żądanie w hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="5d7cb-161">*{Operacja} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe produktu do} & userId = {użytkownika zgłaszającego żądanie} & ziarna = {ciąg} & sig = {ciąg}*</span><span class="sxs-lookup"><span data-stu-id="5d7cb-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="5d7cb-162">Parametry zapytania w przypadku subskrypcji produktu hello:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="5d7cb-163">**Operacja**: Określa, jakiego typu żądanie delegowania jest.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="5d7cb-164">Dla subskrypcji produktu żądań hello prawidłowe opcje to:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="5d7cb-165">"Subskrypcji": toosubscribe żądania hello tooa użytkownika danego produktu o podany identyfikator (patrz poniżej)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="5d7cb-166">"Anuluj subskrypcję": toounsubscribe żądań użytkowników z produktu</span><span class="sxs-lookup"><span data-stu-id="5d7cb-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="5d7cb-167">"Odnowić": toorenew requst subskrypcją (np. może być wygasa)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="5d7cb-168">**productId**: toosubscribe do żądany identyfikator hello hello produktu hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="5d7cb-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="5d7cb-169">**Identyfikator userId**: hello identyfikator hello użytkownika, dla którego hello żądań</span><span class="sxs-lookup"><span data-stu-id="5d7cb-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="5d7cb-170">**ziarna**: specjalne ciąg zaburzający używane do obliczania skrótu zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5d7cb-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="5d7cb-171">**SIG**: obliczona zabezpieczeń toobe wyznaczania wartości skrótu, używany do porównania tooyour własnych obliczoną wartość mieszania</span><span class="sxs-lookup"><span data-stu-id="5d7cb-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="5d7cb-172">Sprawdź, czy Żądanie hello pochodzi z usługi Azure API Management (opcjonalne, lecz zdecydowanie zalecane dla zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="5d7cb-173">Obliczeniowe SHA512 HMAC ciągu oparte na powitania **productId**, **userId** i **soli** parametry zapytania:</span><span class="sxs-lookup"><span data-stu-id="5d7cb-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="5d7cb-174">Metoda HMAC (**soli** + "\n" + **productId** + "\n" + **userId**)</span><span class="sxs-lookup"><span data-stu-id="5d7cb-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="5d7cb-175">Porównaj wartości toohello obliczonego powyżej skrótu hello hello **sig** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="5d7cb-176">Jeśli skróty dwóch hello są zgodne, przesuń w następnym kroku toohello, w przeciwnym razie odmowy żądania hello.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="5d7cb-177">Przetwarzania żadnych subskrypcji produktu oparty na typie hello operacji w **operacji** -np. rozliczeń, dalsze pytania itp.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="5d7cb-178">W subskrypcji pomyślnie hello użytkownika toohello produktu na Twojej stronie, subskrypcja hello użytkownika toohello interfejsu API produktów do zarządzania przez [hello wywołania interfejsu API REST dla subskrypcji produktu].</span><span class="sxs-lookup"><span data-stu-id="5d7cb-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="5d7cb-179"><a name="delegate-example-code"></a> Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="5d7cb-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="5d7cb-180">Pokaż przykłady te kodu jak tootake hello *klucz sprawdzania poprawności delegowania*, który wynosi hello delegowania ekranie powitania wydawcy portalu, toocreate HMAC, który jest następnie używany toovalidate hello podpisu, co dowodzi hello ważności hello przekazany returnUrl.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="5d7cb-181">Witaj, sam kod działa hello productId i userId nieznaczne modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="5d7cb-182">**C# kodu toogenerate skrót returnUrl**</span><span class="sxs-lookup"><span data-stu-id="5d7cb-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="5d7cb-183">**Skrót toogenerate kodu NodeJS returnUrl**</span><span class="sxs-lookup"><span data-stu-id="5d7cb-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="5d7cb-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d7cb-184">Next steps</span></span>
<span data-ttu-id="5d7cb-185">Aby uzyskać więcej informacji na delegowania Zobacz powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="5d7cb-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[żądania tokenu (rejestracji jednokrotnej SSO) single-sign-on]: http://go.microsoft.com/fwlink/?LinkId=507409
[Utwórz użytkownika]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello wywołania interfejsu API REST dla subskrypcji produktu]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[przykładowy kod podany poniżej]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
