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
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a>Kod współpracy usługi Azure Active Directory B2B i przykłady środowiska PowerShell

## <a name="powershell-example"></a>Przykład środowiska PowerShell
Użytkownik może zbiorczego — zaproszenie organizacji tooan użytkowników zewnętrznych z adresów e-mail, które mają być przechowywane w. Plik CSV.

1. Przygotuj hello. CSV plików Utwórz nowy plik CSV i nadaj mu nazwę invitations.csv. W tym przykładzie hello plik jest zapisywany w C:\Data i zawiera hello następujących informacji:
  
  Nazwa                  |  InvitedUserEmailAddress
  --------------------- | --------------------------
  Osoby zaproszonej B2B usługi Gmail     | b2binvitee@gmail.com
  Osoby zaproszonej B2B programu Outlook   | b2binvitee@outlook.com


2. Pobierz najnowsze toouse programu Azure AD PowerShell hello hello nowe polecenia cmdlet, należy zainstalować moduł programu PowerShell usługi Azure AD hello aktualizacji, który można pobrać z [hello stronę wersji modułu programu Powershell](https://www.powershellgallery.com/packages/AzureADPreview)

3. Zaloguj się tooyour dzierżawy

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. Uruchom polecenie cmdlet programu PowerShell hello

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

To polecenie cmdlet wysyła zaproszenie toohello adresy e-mail w invitations.csv. Dodatkowe funkcje tego polecenia cmdlet:
- Tekst wiadomości e-mail hello
- W tym nazwę wyświetlaną dla hello zaproszonych użytkowników
- Wysyłanie wiadomości tooCCs lub całkowicie pomijanie wiadomości e-mail

## <a name="code-sample"></a>Przykład kodu
W tym miejscu możemy pokazują, jak toocall hello zaproszenia interfejsu API, w trybie "tylko do aplikacji", tooget hello realizacji adres URL hello toowhich zasobów, które są zapraszanie hello B2B użytkownika. Celem Hello jest toosend wiadomość e-mail z zaproszeniem niestandardowych. mogą być składane Hello poczty e-mail za pomocą klienta HTTP, więc można dostosować, jak wygląda i wysłać go za pomocą interfejsu API programu Graph.

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


## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
