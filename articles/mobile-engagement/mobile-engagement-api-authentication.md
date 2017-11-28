---
title: "aaaAuthenticate z interfejsów API REST usługi Engagement Mobile"
description: "Opisuje sposób tooauthenticate z interfejsów API REST usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="95f6f-103">Uwierzytelniania za pomocą interfejsów API REST usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="95f6f-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="95f6f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="95f6f-104">Overview</span></span>
<span data-ttu-id="95f6f-105">W tym dokumencie opisano, jak tooget prawidłowy Oauth AAD token tooauthenticate z hello interfejsów API REST usługi Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="95f6f-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="95f6f-106">Zakłada się, że masz ważnej subskrypcji platformy Azure i utworzono aplikację usługi Mobile Engagement, przy użyciu jednej z naszych [samouczki Developer](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="95f6f-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="95f6f-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="95f6f-107">Authentication</span></span>
<span data-ttu-id="95f6f-108">Microsoft Azure Active Directory na podstawie tokenu jest używany do uwierzytelniania OAuth.</span><span class="sxs-lookup"><span data-stu-id="95f6f-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="95f6f-109">Zamówienie tooauthentication interfejsu API nagłówek uwierzytelnienia muszą zostać dodane tooevery żądania, które jest hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="95f6f-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="95f6f-110">Azure Active Directory tokeny wygaśnie w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="95f6f-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="95f6f-111">Istnieje kilka sposobów tooget tokenu.</span><span class="sxs-lookup"><span data-stu-id="95f6f-111">There are several ways tooget a token.</span></span> <span data-ttu-id="95f6f-112">Ponieważ powitalne interfejsy API są zwykle nazywane z usługi w chmurze ma toouse klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="95f6f-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="95f6f-113">Klucz interfejsu API w terminologii Azure jest nazywany hasło główną usługi.</span><span class="sxs-lookup"><span data-stu-id="95f6f-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="95f6f-114">Witaj Poniższa procedura opisuje jednokierunkowej toosetting go ręcznie w górę.</span><span class="sxs-lookup"><span data-stu-id="95f6f-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="95f6f-115">Jednorazowej konfiguracji (przy użyciu skryptu)</span><span class="sxs-lookup"><span data-stu-id="95f6f-115">One-time setup (using script)</span></span>
<span data-ttu-id="95f6f-116">Należy stosować hello zestaw instrukcji poniżej tooperform hello Instalatora za pomocą skryptu programu PowerShell, który przyjmuje hello minimalny czas instalacji, ale używa hello najbardziej dopuszczalnej wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="95f6f-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="95f6f-117">Opcjonalnie można również wykonać instrukcje hello hello [instalacji ręcznej](mobile-engagement-api-authentication-manual.md) Aby to zrobić z hello bezpośrednio portalu Azure i są bardziej precyzyjną konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="95f6f-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="95f6f-118">Pobierz najnowszą wersję programu Azure PowerShell z hello [tutaj](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="95f6f-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="95f6f-119">Aby uzyskać więcej informacji na powitania instrukcje pobierania widać to [łącze](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95f6f-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="95f6f-120">Po zainstalowaniu programu Azure PowerShell, użyj następujących hello polecenia tooensure, że masz hello **modułu Azure** zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="95f6f-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="95f6f-121">a.</span><span class="sxs-lookup"><span data-stu-id="95f6f-121">a.</span></span> <span data-ttu-id="95f6f-122">Upewnij się, że hello modułu Azure PowerShell jest dostępny w hello listę dostępnych modułów.</span><span class="sxs-lookup"><span data-stu-id="95f6f-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Dostępne moduły Azure][1]
   
    <span data-ttu-id="95f6f-124">b.</span><span class="sxs-lookup"><span data-stu-id="95f6f-124">b.</span></span> <span data-ttu-id="95f6f-125">Jeśli nie znajdziesz modułu Azure PowerShell hello hello powyżej listy należy toorun hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="95f6f-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="95f6f-126">Toohello logowania usługi Azure Resource Manager z programu PowerShell, uruchamiając hello następujące polecenia i podając nazwę użytkownika i hasło dla konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="95f6f-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="95f6f-127">Jeśli masz wiele subskrypcji należy uruchomić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="95f6f-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="95f6f-128">a.</span><span class="sxs-lookup"><span data-stu-id="95f6f-128">a.</span></span> <span data-ttu-id="95f6f-129">Pobierz listę subskrypcji i hello kopii subskrypcji o identyfikatorze subskrypcji hello, który ma toouse.</span><span class="sxs-lookup"><span data-stu-id="95f6f-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="95f6f-130">Upewnij się, że ta subskrypcja jest hello takie same, który ma hello Mobile Engagement aplikacji, która ma toointeract przy użyciu hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="95f6f-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="95f6f-131">b.</span><span class="sxs-lookup"><span data-stu-id="95f6f-131">b.</span></span> <span data-ttu-id="95f6f-132">Witaj uruchom następujące polecenie udostępnienie hello SubscriptionId tooconfigure hello subskrypcji toobe używane.</span><span class="sxs-lookup"><span data-stu-id="95f6f-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="95f6f-133">Skopiuj tekst hello hello [AzureRmServicePrincipalOwner.ps1 nowy](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) skryptu tooyour komputera lokalnego i zapisz go jako polecenia cmdlet programu PowerShell (np. `APIAuth.ps1`) i wykonaj go `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="95f6f-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="95f6f-134">Witaj skrypt wyświetli monit tooprovide jako dane wejściowe dla **principalName**.</span><span class="sxs-lookup"><span data-stu-id="95f6f-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="95f6f-135">Podaj odpowiednią nazwę mają toouse toocreate aplikacji usługi Active Directory (np. APIAuth).</span><span class="sxs-lookup"><span data-stu-id="95f6f-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="95f6f-136">Po ukończeniu działania skryptu hello zostaną wyświetlone następujące cztery wartości, które będą potrzebne hello tooauthenticate programowo z usługą Active Directory, dlatego upewnij się, że toocopy je.</span><span class="sxs-lookup"><span data-stu-id="95f6f-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="95f6f-137">**TenantId**, **SubscriptionId**, **ApplicationId**, i **klucz tajny**.</span><span class="sxs-lookup"><span data-stu-id="95f6f-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="95f6f-138">Użyje TenantId jako `{TENANT_ID}`, identyfikator aplikacji jako `{CLIENT_ID}` i tajne jako `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="95f6f-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95f6f-139">Domyślne zasady zabezpieczeń blokują uruchomionych skryptów PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95f6f-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="95f6f-140">Jeśli tak, należy skonfigurować tymczasowo z zasad wykonywania tooallow wykonywanie skryptu za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="95f6f-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="95f6f-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="95f6f-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="95f6f-142">Oto jak będzie wyglądać hello zestaw poleceń cmdlet środowiska PS.</span><span class="sxs-lookup"><span data-stu-id="95f6f-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="95f6f-143">Sprawdź w portalu zarządzania Azure hello nową aplikację usługi AD utworzenia o nazwie hello zostanie podane nazywany toohello skryptu **principalName** w obszarze **Pokaż aplikacje Moja firma jest właścicielem**.</span><span class="sxs-lookup"><span data-stu-id="95f6f-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="95f6f-144">Kroki tooget prawidłowy token</span><span class="sxs-lookup"><span data-stu-id="95f6f-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="95f6f-145">Wywołanie interfejsu API hello z hello następujące parametry i upewnij się, że tooreplace hello dzierżawy\_identyfikator, klient\_identyfikator i klienta\_klucz TAJNY:</span><span class="sxs-lookup"><span data-stu-id="95f6f-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="95f6f-146">**Adres URL żądania** jako *https://login.microsoftonline.com/ {dzierżawy\_identyfikator} / oauth2/token.*</span><span class="sxs-lookup"><span data-stu-id="95f6f-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="95f6f-147">**Nagłówek HTTP Content-Type** jako *application/x--www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="95f6f-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="95f6f-148">**Treść żądania HTTP** jako *przyznać\_typu = klient\_poświadczenia & client_id = {klienta\_identyfikator} & client_secret = {klienta\_klucz TAJNY} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="95f6f-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="95f6f-149">Witaj poniżej przedstawiono przykładowe żądanie:</span><span class="sxs-lookup"><span data-stu-id="95f6f-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="95f6f-150">POST / {TENANT_ID} / oauth2/token hostów protokołu HTTP/1.1: login.microsoftonline.com Content-Type: application/x--www-form-urlencoded typ grant_type = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & staw nazw = https % 3A % 2f%2Fmanagement.Core.Windows.NET%2f</span><span class="sxs-lookup"><span data-stu-id="95f6f-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="95f6f-151">Oto przykład odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="95f6f-151">Here is an example response:</span></span>
     
       <span data-ttu-id="95f6f-152">HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8 Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="95f6f-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="95f6f-153">{"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911 zasobu","": "https://management.core.windows.net/", "' access_token '": {' access_token '}}</span><span class="sxs-lookup"><span data-stu-id="95f6f-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="95f6f-154">W tym przykładzie uwzględnione hello parametrów POST, podczas kodowania adresu URL `resource` wartość jest rzeczywiście `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="95f6f-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="95f6f-155">Należy zachować ostrożność, kodowania adresu URL tooalso `{CLIENT_SECRET}` jako może zawierać znaków specjalnych.</span><span class="sxs-lookup"><span data-stu-id="95f6f-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="95f6f-156">Do testowania, można użyć narzędzia klienta HTTP, takiego jak [Fiddler](http://www.telerik.com/fiddler) lub [rozszerzenia Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="95f6f-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="95f6f-157">W każdym wywołaniu interfejsu API zawierają teraz nagłówek żądania autoryzacji hello:</span><span class="sxs-lookup"><span data-stu-id="95f6f-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="95f6f-158">Jeśli zostanie wyświetlony kod stanu 401 zwrócone, sprawdź treść odpowiedzi hello, jego może poinformować użytkownika hello token utracił ważność.</span><span class="sxs-lookup"><span data-stu-id="95f6f-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="95f6f-159">W takim przypadku należy uzyskać nowy token.</span><span class="sxs-lookup"><span data-stu-id="95f6f-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="95f6f-160">Przy użyciu hello interfejsów API</span><span class="sxs-lookup"><span data-stu-id="95f6f-160">Using hello APIs</span></span>
<span data-ttu-id="95f6f-161">Użytkownik ma prawidłowy token, użytkownik jest gotowy toomake wywołania hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="95f6f-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="95f6f-162">W poszczególnych żądań interfejsu API konieczne będzie toopass prawidłowych, niewygasłych tokenem, który został uzyskany w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="95f6f-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="95f6f-163">Należy tooplug w niektórych parametrów do żądania hello identyfikator URI, który identyfikuje aplikację.</span><span class="sxs-lookup"><span data-stu-id="95f6f-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="95f6f-164">Identyfikator URI żądania Hello wygląda hello</span><span class="sxs-lookup"><span data-stu-id="95f6f-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="95f6f-165">Parametry hello tooget, kliknij nazwę aplikacji i kliknij pozycję pulpit nawigacyjny i zostanie wyświetlona strona, takie jak następujące hello ze wszystkimi hello 3 parametry.</span><span class="sxs-lookup"><span data-stu-id="95f6f-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="95f6f-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="95f6f-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="95f6f-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="95f6f-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="95f6f-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="95f6f-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="95f6f-169">**4** nazwy grupy zasobów your będzie toobe **MobileEngagement** chyba że zostaną utworzone nowe.</span><span class="sxs-lookup"><span data-stu-id="95f6f-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parametry identyfikatora URI interfejsu API usługi Engagement Mobile][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="95f6f-171">Ignoruj hello adres głównego interfejsu API, jak to uzyskać hello poprzedniej interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="95f6f-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="95f6f-172">Jeśli utworzono aplikację hello przy użyciu klasycznego portalu Azure należy nazwy zasobu usługi Application hello toouse, która jest inna niż nazwa aplikacji hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="95f6f-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="95f6f-173">Jeśli utworzono aplikację hello w hello portalu Azure należy używać hello Nazwa aplikacji (brak rozróżnienia między nazwa zasobów aplikacji i nazwy aplikacji dla aplikacji utworzonych w hello nowego portalu).</span><span class="sxs-lookup"><span data-stu-id="95f6f-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



