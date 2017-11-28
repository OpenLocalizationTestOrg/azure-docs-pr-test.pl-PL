---
title: "aaaAzure Active Directory B2B kod współpracy i przykłady środowiska PowerShell | Dokumentacja firmy Microsoft"
description: "Przykłady kodu i programu PowerShell dla usługi Azure Active Directory B2B współpracy"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 8e4f66fcb50d190899304831ea7ccd2203c5468c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a><span data-ttu-id="c84f7-103">Kod współpracy usługi Azure Active Directory B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="c84f7-103">Azure Active Directory B2B collaboration code and PowerShell samples</span></span>

## <a name="powershell-example"></a><span data-ttu-id="c84f7-104">Przykład środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="c84f7-104">PowerShell example</span></span>
<span data-ttu-id="c84f7-105">Użytkownik może zbiorczego — zaproszenie organizacji tooan użytkowników zewnętrznych z adresów e-mail, które mają być przechowywane w. Plik CSV.</span><span class="sxs-lookup"><span data-stu-id="c84f7-105">You can bulk-invite external users tooan organization from email addresses that you have stored in a .CSV file.</span></span>

1. <span data-ttu-id="c84f7-106">Przygotuj hello. CSV plików Utwórz nowy plik CSV i nadaj mu nazwę invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="c84f7-106">Prepare hello .CSV file Create a new CSV file and name it invitations.csv.</span></span> <span data-ttu-id="c84f7-107">W tym przykładzie hello plik jest zapisywany w C:\Data i zawiera hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="c84f7-107">In this example, hello file is saved in C:\data, and contains hello following information:</span></span>
  
  <span data-ttu-id="c84f7-108">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c84f7-108">Name</span></span>                  |  <span data-ttu-id="c84f7-109">InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="c84f7-109">InvitedUserEmailAddress</span></span>
  --------------------- | --------------------------
  <span data-ttu-id="c84f7-110">Osoby zaproszonej B2B usługi Gmail</span><span class="sxs-lookup"><span data-stu-id="c84f7-110">Gmail B2B Invitee</span></span>     | b2binvitee@gmail.com
  <span data-ttu-id="c84f7-111">Osoby zaproszonej B2B programu Outlook</span><span class="sxs-lookup"><span data-stu-id="c84f7-111">Outlook B2B invitee</span></span>   | b2binvitee@outlook.com


2. <span data-ttu-id="c84f7-112">Pobierz najnowsze toouse programu Azure AD PowerShell hello hello nowe polecenia cmdlet, należy zainstalować moduł programu PowerShell usługi Azure AD hello aktualizacji, który można pobrać z [hello stronę wersji modułu programu Powershell](https://www.powershellgallery.com/packages/AzureADPreview)</span><span class="sxs-lookup"><span data-stu-id="c84f7-112">Get hello latest Azure AD PowerShell toouse hello new cmdlets, you must install hello updated Azure AD PowerShell module, which you can download from [hello Powershell module's release page](https://www.powershellgallery.com/packages/AzureADPreview)</span></span>

3. <span data-ttu-id="c84f7-113">Zaloguj się tooyour dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c84f7-113">Sign in tooyour tenancy</span></span>

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. <span data-ttu-id="c84f7-114">Uruchom polecenie cmdlet programu PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="c84f7-114">Run hello PowerShell cmdlet</span></span>

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

<span data-ttu-id="c84f7-115">To polecenie cmdlet wysyła zaproszenie toohello adresy e-mail w invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="c84f7-115">This cmdlet sends an invitation toohello email addresses in invitations.csv.</span></span> <span data-ttu-id="c84f7-116">Dodatkowe funkcje tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c84f7-116">Additional features of this cmdlet include:</span></span>
- <span data-ttu-id="c84f7-117">Tekst wiadomości e-mail hello</span><span class="sxs-lookup"><span data-stu-id="c84f7-117">Customized text in hello email message</span></span>
- <span data-ttu-id="c84f7-118">W tym nazwę wyświetlaną dla hello zaproszonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c84f7-118">Including a display name for hello invited user</span></span>
- <span data-ttu-id="c84f7-119">Wysyłanie wiadomości tooCCs lub całkowicie pomijanie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="c84f7-119">Sending messages tooCCs or suppressing email messages altogether</span></span>

## <a name="code-sample"></a><span data-ttu-id="c84f7-120">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="c84f7-120">Code sample</span></span>
<span data-ttu-id="c84f7-121">W tym miejscu możemy pokazują, jak toocall hello zaproszenia interfejsu API, w trybie "tylko do aplikacji", tooget hello realizacji adres URL hello toowhich zasobów, które są zapraszanie hello B2B użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c84f7-121">Here we illustrate how toocall hello invitation API, in "app-only" mode, tooget hello redemption URL for hello resource toowhich you are inviting hello B2B user.</span></span> <span data-ttu-id="c84f7-122">Celem Hello jest toosend wiadomość e-mail z zaproszeniem niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c84f7-122">hello goal is toosend a custom invitation email.</span></span> <span data-ttu-id="c84f7-123">mogą być składane Hello poczty e-mail za pomocą klienta HTTP, więc można dostosować, jak wygląda i wysłać go za pomocą interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="c84f7-123">hello email can be composed with an HTTP client, so you can customize how it looks and send it through Graph API.</span></span>

```
namespace SampleInviteApp
{
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    class Program
    {
        /// <summary>
        /// Microsoft graph resource.
        /// </summary>
        static readonly string GraphResource = "https://graph.microsoft.com";
 
        /// <summary>
        /// Microsoft graph invite endpoint.
        /// </summary>
        static readonly string InviteEndPoint = "https://graph.microsoft.com/v1.0/invitations";
 
        /// <summary>
        ///  Authentication endpoint tooget token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is hello tenantid of hello tenant you want tooinvite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is hello application id of hello application that is registered in hello above tenant.
        /// hello required scopes are available in hello below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of hello application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is hello email address of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is hello display name of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserDisplayName = @"";
 
        /// <summary>
        /// Main method.
        /// </summary>
        /// <param name="args">Optional arguments</param>
        static void Main(string[] args)
        {
            Invitation invitation = CreateInvitation();
            SendInvitation(invitation);
        }
 
        /// <summary>
        /// Create hello invitation object.
        /// </summary>
        /// <returns>Returns hello invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set hello invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send hello guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make hello invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get hello HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns hello Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for hello request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get hello access token for our application tootalk toomicrosoft graph.
        /// </summary>
        /// <returns>Returns hello access token for our application tootalk toomicrosoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get hello access token for our application tootalk toomicrosoft graph.
            try
            {
                AuthenticationContext testAuthContext =
                    new AuthenticationContext(string.Format("{0}/{1}", EstsLoginEndpoint, TenantID));
                AuthenticationResult testAuthResult = testAuthContext.AcquireTokenAsync(
                    GraphResource,
                    new ClientCredential(TestAppClientId, TestAppClientSecret)).Result;
                accessToken = testAuthResult.AccessToken;
            }
            catch (AdalException ex)
            {
                Console.WriteLine("An exception was thrown while fetching hello token: {0}.", ex);
                throw;
            }
 
            return accessToken;
        }
 
        /// <summary>
        /// Invitation class.
        /// </summary>
        public class Invitation
        {
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserDisplayName { get; set; }
 
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserEmailAddress { get; set; }
 
            /// <summary>
            /// Gets or sets a value indicating whether Invitation Manager should send hello email tooInvitedUser.
            /// </summary>
            public bool SendInvitationMessage { get; set; }
 
            /// <summary>
            /// Gets or sets invitation redirect URL
            /// </summary>
            public string InviteRedirectUrl { get; set; }
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="c84f7-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c84f7-124">Next steps</span></span>

<span data-ttu-id="c84f7-125">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c84f7-125">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c84f7-126">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c84f7-126">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c84f7-127">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-127">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c84f7-128">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-128">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c84f7-129">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-129">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c84f7-130">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-130">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c84f7-131">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c84f7-132">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c84f7-133">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="c84f7-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c84f7-134">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="c84f7-134">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c84f7-135">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c84f7-135">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
