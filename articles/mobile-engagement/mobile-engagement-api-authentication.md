---
title: "Uwierzytelniania za pomocą interfejsów API REST usługi Mobile Engagement"
description: "Opisuje sposób uwierzytelniania za pomocą interfejsów API REST usługi Azure Mobile Engagement"
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
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="afe5c-103">Uwierzytelniania za pomocą interfejsów API REST usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="afe5c-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="afe5c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="afe5c-104">Overview</span></span>
<span data-ttu-id="afe5c-105">Ten dokument zawiera opis sposobu uzyskać prawidłowy Oauth AAD token uwierzytelniania za pomocą interfejsów API REST Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="afe5c-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="afe5c-106">Zakłada się, że masz ważnej subskrypcji platformy Azure i utworzono aplikację usługi Mobile Engagement, przy użyciu jednej z naszych [samouczki Developer](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="afe5c-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="afe5c-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="afe5c-107">Authentication</span></span>
<span data-ttu-id="afe5c-108">Microsoft Azure Active Directory na podstawie tokenu jest używany do uwierzytelniania OAuth.</span><span class="sxs-lookup"><span data-stu-id="afe5c-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="afe5c-109">Aby żądania uwierzytelnienia interfejsu API nagłówek autoryzacji muszą być dodane do każdego żądania, który jest następujący:</span><span class="sxs-lookup"><span data-stu-id="afe5c-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="afe5c-110">Azure Active Directory tokeny wygaśnie w ciągu godziny.</span><span class="sxs-lookup"><span data-stu-id="afe5c-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="afe5c-111">Istnieje kilka sposobów w celu pobrania tokenu.</span><span class="sxs-lookup"><span data-stu-id="afe5c-111">There are several ways to get a token.</span></span> <span data-ttu-id="afe5c-112">Ponieważ interfejsy API są zwykle nazywane z usługi w chmurze, ma być używany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="afe5c-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="afe5c-113">Klucz interfejsu API w terminologii Azure jest nazywany hasło główną usługi.</span><span class="sxs-lookup"><span data-stu-id="afe5c-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="afe5c-114">W poniższej procedurze opisano jeden ze sposobów konfigurowania go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="afe5c-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="afe5c-115">Jednorazowej konfiguracji (przy użyciu skryptu)</span><span class="sxs-lookup"><span data-stu-id="afe5c-115">One-time setup (using script)</span></span>
<span data-ttu-id="afe5c-116">Należy stosować zestaw instrukcjami poniżej, aby przeprowadzić instalację za pomocą skryptu programu PowerShell, co ma minimalny czas instalacji, ale używa najbardziej dopuszczalnej wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="afe5c-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="afe5c-117">Opcjonalnie można również wykonać instrukcje w [instalacji ręcznej](mobile-engagement-api-authentication-manual.md) Aby to zrobić bezpośrednio portalu Azure i są bardziej precyzyjną konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afe5c-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="afe5c-118">Pobierz najnowszą wersję programu Azure PowerShell z [tutaj](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="afe5c-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="afe5c-119">Aby uzyskać więcej informacji na instrukcje pobierania widać to [łącze](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="afe5c-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="afe5c-120">Po zainstalowaniu programu Azure PowerShell, użyj następujących poleceń, aby upewnić się, że masz **modułu Azure** zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="afe5c-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="afe5c-121">a.</span><span class="sxs-lookup"><span data-stu-id="afe5c-121">a.</span></span> <span data-ttu-id="afe5c-122">Upewnij się, że moduł Azure PowerShell jest dostępny na liście dostępnych modułów.</span><span class="sxs-lookup"><span data-stu-id="afe5c-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Dostępne moduły Azure][1]
   
    <span data-ttu-id="afe5c-124">b.</span><span class="sxs-lookup"><span data-stu-id="afe5c-124">b.</span></span> <span data-ttu-id="afe5c-125">Jeśli nie zostanie znaleziony moduł Azure PowerShell w powyższej listy, a następnie należy uruchomić następujące:</span><span class="sxs-lookup"><span data-stu-id="afe5c-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="afe5c-126">Logowanie do usługi Azure Resource Manager z programu PowerShell, uruchom następujące polecenie i podając nazwę użytkownika i hasło dla konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="afe5c-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="afe5c-127">Jeśli masz wiele subskrypcji należy uruchomić następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="afe5c-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="afe5c-128">a.</span><span class="sxs-lookup"><span data-stu-id="afe5c-128">a.</span></span> <span data-ttu-id="afe5c-129">Pobranie listy wszystkich subskrypcji, a następnie skopiuj element SubscriptionId subskrypcję, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="afe5c-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="afe5c-130">Upewnij się, że ta subskrypcja jest taka sama jak mającej Mobile Engagement App, w którym będą wchodzić w interakcje z użyciem interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="afe5c-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="afe5c-131">b.</span><span class="sxs-lookup"><span data-stu-id="afe5c-131">b.</span></span> <span data-ttu-id="afe5c-132">Uruchom następujące polecenie podając identyfikator subskrypcji do konfigurowania subskrypcji do użycia.</span><span class="sxs-lookup"><span data-stu-id="afe5c-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="afe5c-133">Skopiuj tekst [AzureRmServicePrincipalOwner.ps1 nowy](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) skryptu na komputerze lokalnym i zapisz go jako polecenia cmdlet programu PowerShell (np. `APIAuth.ps1`) i wykonaj go `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="afe5c-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="afe5c-134">Skrypt zostanie wyświetlony monit o podanie danych wejściowych dla **principalName**.</span><span class="sxs-lookup"><span data-stu-id="afe5c-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="afe5c-135">Podaj odpowiednią nazwę chcesz używać do tworzenia aplikacji usługi Active Directory (np. APIAuth).</span><span class="sxs-lookup"><span data-stu-id="afe5c-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="afe5c-136">Po ukończeniu działania skryptu, zostaną wyświetlone następujące cztery wartości, które będą potrzebne do uwierzytelnienia programowo z usługą Active Directory tak upewnij się, że skopiuj je.</span><span class="sxs-lookup"><span data-stu-id="afe5c-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="afe5c-137">**TenantId**, **SubscriptionId**, **ApplicationId**, i **klucz tajny**.</span><span class="sxs-lookup"><span data-stu-id="afe5c-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="afe5c-138">Użyje TenantId jako `{TENANT_ID}`, identyfikator aplikacji jako `{CLIENT_ID}` i tajne jako `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="afe5c-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="afe5c-139">Domyślne zasady zabezpieczeń blokują uruchomionych skryptów PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afe5c-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="afe5c-140">Jeśli tak, tymczasowo należy skonfigurować zasady wykonywania, aby pozwolić na wykonanie skryptu za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="afe5c-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="afe5c-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="afe5c-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="afe5c-142">Oto jak będzie wyglądać zestaw poleceń cmdlet środowiska PS.</span><span class="sxs-lookup"><span data-stu-id="afe5c-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="afe5c-143">Sprawdź w portalu zarządzania Azure utworzenia nowej aplikacji usługi AD o nazwie dostarczone do skryptu o nazwie **principalName** w obszarze **Pokaż aplikacje Moja firma jest właścicielem**.</span><span class="sxs-lookup"><span data-stu-id="afe5c-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="afe5c-144">Kroki, aby pobrać prawidłowego tokenu</span><span class="sxs-lookup"><span data-stu-id="afe5c-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="afe5c-145">Wywołanie interfejsu API z następującymi parametrami i upewnij się zastąpić DZIERŻAWCY\_identyfikator, klient\_identyfikator i klienta\_klucz TAJNY:</span><span class="sxs-lookup"><span data-stu-id="afe5c-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="afe5c-146">**Adres URL żądania** jako *https://login.microsoftonline.com/ {dzierżawy\_identyfikator} / oauth2/token.*</span><span class="sxs-lookup"><span data-stu-id="afe5c-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="afe5c-147">**Nagłówek HTTP Content-Type** jako *application/x--www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="afe5c-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="afe5c-148">**Treść żądania HTTP** jako *przyznać\_typu = klient\_poświadczenia & client_id = {klienta\_identyfikator} & client_secret = {klienta\_klucz TAJNY} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="afe5c-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="afe5c-149">Poniżej zamieszczono przykładowe żądanie:</span><span class="sxs-lookup"><span data-stu-id="afe5c-149">The following is an example request:</span></span>
     
       <span data-ttu-id="afe5c-150">POST / {TENANT_ID} / oauth2/token hostów protokołu HTTP/1.1: login.microsoftonline.com Content-Type: application/x--www-form-urlencoded typ grant_type = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & staw nazw = https % 3A % 2f%2Fmanagement.Core.Windows.NET%2f</span><span class="sxs-lookup"><span data-stu-id="afe5c-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="afe5c-151">Oto przykład odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="afe5c-151">Here is an example response:</span></span>
     
       <span data-ttu-id="afe5c-152">HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8 Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="afe5c-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="afe5c-153">{"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911 zasobu","": "https://management.core.windows.net/", "' access_token '": {' access_token '}}</span><span class="sxs-lookup"><span data-stu-id="afe5c-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="afe5c-154">W tym przykładzie uwzględnione podczas kodowania adresu URL parametrów POST `resource` wartość jest rzeczywiście `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="afe5c-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="afe5c-155">Należy zachować ostrożność, jak również adres URL kodowania `{CLIENT_SECRET}` jako może zawierać znaków specjalnych.</span><span class="sxs-lookup"><span data-stu-id="afe5c-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="afe5c-156">Do testowania, można użyć narzędzia klienta HTTP, takiego jak [Fiddler](http://www.telerik.com/fiddler) lub [rozszerzenia Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="afe5c-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="afe5c-157">W każdym wywołaniu interfejsu API zawierają teraz nagłówek żądania autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="afe5c-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="afe5c-158">Jeśli otrzymasz zwrócił kod stanu 401, sprawdź treść odpowiedzi go mogą informować o token utracił ważność.</span><span class="sxs-lookup"><span data-stu-id="afe5c-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="afe5c-159">W takim przypadku należy uzyskać nowy token.</span><span class="sxs-lookup"><span data-stu-id="afe5c-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="afe5c-160">Korzystanie z interfejsów API</span><span class="sxs-lookup"><span data-stu-id="afe5c-160">Using the APIs</span></span>
<span data-ttu-id="afe5c-161">Teraz, gdy masz prawidłowy token, można przystąpić do wykonywania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="afe5c-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="afe5c-162">W poszczególnych żądań interfejsu API należy przekazać token prawidłowych, niewygasłych uzyskaną w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="afe5c-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="afe5c-163">Należy podłączyć niektórych parametrów w żądaniu identyfikatora URI, który identyfikuje aplikację.</span><span class="sxs-lookup"><span data-stu-id="afe5c-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="afe5c-164">Żądanie identyfikatora URI wygląda następująco</span><span class="sxs-lookup"><span data-stu-id="afe5c-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="afe5c-165">Aby pobrać parametrów, kliknij nazwę aplikacji i kliknij pulpit nawigacyjny i zostanie wyświetlona strona podobnie do następującej z 3 parametry.</span><span class="sxs-lookup"><span data-stu-id="afe5c-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="afe5c-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="afe5c-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="afe5c-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="afe5c-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="afe5c-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="afe5c-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="afe5c-169">**4** nazwy Twojej grupy zasobów ma być **MobileEngagement** chyba że zostaną utworzone nowe.</span><span class="sxs-lookup"><span data-stu-id="afe5c-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parametry identyfikatora URI interfejsu API usługi Engagement Mobile][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="afe5c-171">Ignoruj adres głównego interfejsu API, jak to dla poprzedniego interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="afe5c-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="afe5c-172">Jeśli utworzono aplikację przy użyciu klasycznego portalu Azure należy użyć nazwy zasobu aplikacji, która jest inna niż nazwa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afe5c-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="afe5c-173">Jeśli utworzono aplikację w portalu Azure należy używać cała nazwa aplikacji (brak rozróżnienia między nazwa zasobów aplikacji i nazwy aplikacji dla aplikacji utworzonych w nowego portalu).</span><span class="sxs-lookup"><span data-stu-id="afe5c-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



