---
title: "Kod współpracy usługi Azure Active Directory B2B i przykłady programu PowerShell | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cae69f57627b3058bf96c3d1eea7dadc81147153
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a><span data-ttu-id="62cc6-103">Kod współpracy usługi Azure Active Directory B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="62cc6-103">Azure Active Directory B2B collaboration code and PowerShell samples</span></span>

## <a name="powershell-example"></a><span data-ttu-id="62cc6-104">Przykład środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="62cc6-104">PowerShell example</span></span>
<span data-ttu-id="62cc6-105">Można można zbiorczego — zaprosić użytkowników zewnętrznych do organizacji z adresów e-mail, które mają być przechowywane w. Plik CSV.</span><span class="sxs-lookup"><span data-stu-id="62cc6-105">You can bulk-invite external users to an organization from email addresses that you have stored in a .CSV file.</span></span>

1. <span data-ttu-id="62cc6-106">Przygotowywanie. CSV plików Utwórz nowy plik CSV i nadaj mu nazwę invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="62cc6-106">Prepare the .CSV file Create a new CSV file and name it invitations.csv.</span></span> <span data-ttu-id="62cc6-107">W tym przykładzie plik zostanie zapisany w C:\Data i zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="62cc6-107">In this example, the file is saved in C:\data, and contains the following information:</span></span>
  
  <span data-ttu-id="62cc6-108">Nazwa</span><span class="sxs-lookup"><span data-stu-id="62cc6-108">Name</span></span>                  |  <span data-ttu-id="62cc6-109">InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="62cc6-109">InvitedUserEmailAddress</span></span>
  --------------------- | --------------------------
  <span data-ttu-id="62cc6-110">Osoby zaproszonej B2B usługi Gmail</span><span class="sxs-lookup"><span data-stu-id="62cc6-110">Gmail B2B Invitee</span></span>     | b2binvitee@gmail.com
  <span data-ttu-id="62cc6-111">Osoby zaproszonej B2B programu Outlook</span><span class="sxs-lookup"><span data-stu-id="62cc6-111">Outlook B2B invitee</span></span>   | b2binvitee@outlook.com


2. <span data-ttu-id="62cc6-112">Pobierz najnowsze programu Azure AD PowerShell posługiwanie się nowymi poleceniami, należy zainstalować zaktualizowaną moduł programu PowerShell usługi Azure AD, który można pobrać z [stronę wersji modułu programu Powershell](https://www.powershellgallery.com/packages/AzureADPreview)</span><span class="sxs-lookup"><span data-stu-id="62cc6-112">Get the latest Azure AD PowerShell To use the new cmdlets, you must install the updated Azure AD PowerShell module, which you can download from [the Powershell module's release page](https://www.powershellgallery.com/packages/AzureADPreview)</span></span>

3. <span data-ttu-id="62cc6-113">Zaloguj się do Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="62cc6-113">Sign in to your tenancy</span></span>

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. <span data-ttu-id="62cc6-114">Uruchom polecenie cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="62cc6-114">Run the PowerShell cmdlet</span></span>

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

<span data-ttu-id="62cc6-115">To polecenie cmdlet wysyła zaproszenia na adresy e-mail w invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="62cc6-115">This cmdlet sends an invitation to the email addresses in invitations.csv.</span></span> <span data-ttu-id="62cc6-116">Dodatkowe funkcje tego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="62cc6-116">Additional features of this cmdlet include:</span></span>
- <span data-ttu-id="62cc6-117">Tekst w wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="62cc6-117">Customized text in the email message</span></span>
- <span data-ttu-id="62cc6-118">W tym nazwę wyświetlaną dla zaproszonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="62cc6-118">Including a display name for the invited user</span></span>
- <span data-ttu-id="62cc6-119">Wysyłanie komunikatów do CCs lub całkowicie pomijanie wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="62cc6-119">Sending messages to CCs or suppressing email messages altogether</span></span>

## <a name="code-sample"></a><span data-ttu-id="62cc6-120">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="62cc6-120">Code sample</span></span>
<span data-ttu-id="62cc6-121">W tym miejscu możemy ilustrują sposób wywołania interfejsu API, zaproszenia w trybie "tylko do aplikacji", aby uzyskać adres URL realizacji dla zasobu, do którego są wyświetli monit o B2B.</span><span class="sxs-lookup"><span data-stu-id="62cc6-121">Here we illustrate how to call the invitation API, in "app-only" mode, to get the redemption URL for the resource to which you are inviting the B2B user.</span></span> <span data-ttu-id="62cc6-122">Celem jest Wyślij wiadomość e-mail z zaproszeniem niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="62cc6-122">The goal is to send a custom invitation email.</span></span> <span data-ttu-id="62cc6-123">Wiadomości e-mail mogą być składane za pomocą klienta HTTP, więc można dostosować, jak wygląda i wysłać go za pomocą interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="62cc6-123">The email can be composed with an HTTP client, so you can customize how it looks and send it through Graph API.</span></span>

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
        ///  Authentication endpoint to get token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is the tenantid of the tenant you want to invite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is the application id of the application that is registered in the above tenant.
        /// The required scopes are available in the below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of the application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is the email address of the user you want to invite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is the display name of the user you want to invite.
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
        /// Create the invitation object.
        /// </summary>
        /// <returns>Returns the invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set the invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send the guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make the invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get the HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns the Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for the request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get the access token for our application to talk to microsoft graph.
        /// </summary>
        /// <returns>Returns the access token for our application to talk to microsoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get the access token for our application to talk to microsoft graph.
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
                Console.WriteLine("An exception was thrown while fetching the token: {0}.", ex);
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
            /// Gets or sets a value indicating whether Invitation Manager should send the email to InvitedUser.
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


## <a name="next-steps"></a><span data-ttu-id="62cc6-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62cc6-124">Next steps</span></span>

<span data-ttu-id="62cc6-125">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="62cc6-125">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="62cc6-126">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="62cc6-126">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="62cc6-127">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-127">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="62cc6-128">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-128">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="62cc6-129">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-129">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="62cc6-130">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-130">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="62cc6-131">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="62cc6-132">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="62cc6-133">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="62cc6-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="62cc6-134">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="62cc6-134">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="62cc6-135">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="62cc6-135">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
