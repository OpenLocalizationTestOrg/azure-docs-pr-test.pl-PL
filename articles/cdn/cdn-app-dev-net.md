---
title: "aaaGet wprowadzenie hello biblioteki usługi Azure CDN dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage aplikacji .NET toowrite Azure CDN przy użyciu programu Visual Studio."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Rozpoczynanie pracy z wdrażaniem usługi Azure CDN
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Można użyć hello [biblioteki usługi Azure CDN dla platformy .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.  Ten samouczek przeprowadzi Cię przez hello tworzenia prostej aplikacji konsoli .NET, która przedstawia niektóre z dostępnych operacji hello.  Ten samouczek jest przeznaczony toodescribe wszystkich aspektów hello biblioteki usługi Azure CDN dla platformy .NET szczegółowo.

Należy toocomplete programu Visual Studio 2015 w tym samouczku.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) jest dostępny do pobrania.

> [!TIP]
> Witaj [ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) jest dostępny do pobrania w witrynie MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Tworzenie projektu i dodawanie pakietów Nuget
Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych profilów usługi CDN toomanage uprawnienia aplikacji usługi Azure AD i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.

W programie Visual Studio 2015, kliknij **pliku**, **nowy**, **projektu...**  tooopen powitalne okno dialogowe nowego projektu.  Rozwiń węzeł **Visual C#**, a następnie wybierz pozycję **Windows** hello okienka po lewej stronie powitania.  Kliknij przycisk **aplikacji konsoli** w okienku Centrum hello.  Nazwij swój projekt, a następnie kliknij przycisk **OK**.  

![Nowy projekt](./media/cdn-app-dev-net/cdn-new-project.png)

Nasze projektu będzie toouse niektóre biblioteki Azure zawartych w pakietach Nuget.  Umożliwia dodanie tych toohello projektu.

1. Kliknij przycisk hello **narzędzia** menu **Menedżera pakietów Nuget**, następnie **Konsola Menedżera pakietów**.
   
    ![Zarządzaj pakietami Nuget](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. W konsoli Menedżera pakietów hello, wykonaj następujące polecenie tooinstall hello hello **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Wykonaj następujące tooinstall hello hello **biblioteki zarządzania usługi Azure CDN**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Dyrektywy, Metoda główna, stałe i metody pomocnicze
Załóż hello podstawowej struktury nasz program zapisywane.

1. Powrót na karcie Program.cs hello, Zastąp hello `using` dyrektywy u góry hello hello poniżej:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. Potrzebujemy toodefine niektóre stałe, używanego przez naszych metod.  W hello `Program` klasy, ale przed hello `Main` metody, Dodaj następujące hello.  Należy się tooreplace symbole zastępcze hello, w tym hello  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Również na poziomie klasy hello, należy zdefiniować te dwie zmienne.  Użyjemy tych toodetermine nowszych Jeśli naszych profilu i punktu końcowego już istnieje.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Zastąp hello `Main` metody w następujący sposób:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Niektóre z naszych innych metod będzie tooprompt hello użytkownika za pomocą pytań "Yes/No".  Dodaj następujące metody toomake hello który nieco łatwiejsze:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Teraz, gdy podstawowa struktura nasz program hello są zapisywane, utworzymy powinien hello metody wywoływane przez hello `Main` metody.

## <a name="authentication"></a>Authentication
Przed możemy użyć hello biblioteki zarządzania usługi Azure CDN, możemy muszą tooauthenticate nasza usługa główna i uzyskiwanie tokenu uwierzytelniania.  Ta metoda używa biblioteki ADAL tooretrieve hello tokenu.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Jeśli używasz uwierzytelniania użytkownika hello `GetAccessToken` metody będą różnić się nieznacznie.

> [!IMPORTANT]
> Ten przykładowy kod należy używać tylko, jeśli użytkownik zdecyduje toohave uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Należy się tooreplace `<redirect URI>` z hello przekierowania URI wprowadzona podczas rejestrowania aplikacji hello w usłudze Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Lista profilów CDN i punkty końcowe
Jest teraz gotowy tooperform operacji CDN.  Hello przede wszystkim naszym metoda wykonuje jest lista wszystkich profilów hello i punktów końcowych w naszej grupy zasobów, a w przypadku odnalezienia pasuje do nazwy profilu i punktu końcowego hello określone w naszym stałe udziela Uwaga tego na później, firma Microsoft nie próbuj toocreate duplikaty.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Tworzenie profilów sieci CDN i punkty końcowe
Następnie utworzymy profilu.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Po utworzeniu profilu hello utworzymy punktu końcowego.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> w powyższym przykładzie Hello przypisuje punktu końcowego hello pochodzenia o nazwie *Contoso* z nazwą hosta `www.contoso.com`.  Należy zmienić nazwę hosta tego toopoint tooyour własnych źródła.
> 
> 

## <a name="purge-an-endpoint"></a>Przeczyszczanie punktu końcowego
Przy założeniu, że utworzono punkt końcowy hello, jednego z typowych zadań, że firma Microsoft może być tooperform w naszym program jest przeczyszczanie hello zawartości w naszym punktu końcowego.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> W powyższym przykładzie hello, hello ciąg `/*` oznacza, że ma być toopurge wszystko w głównym hello hello ścieżkę punktu końcowego.  Jest to równoważne toochecking **przeczyścić wszystkie** w hello portalu Azure "przeczyścić" okna dialogowego. W hello `CreateCdnProfile` metody, po utworzeniu profilu naszych jako **Azure CDN from Verizon** profilu przy użyciu kodu hello `Sku = new Sku(SkuName.StandardVerizon)`, więc to zakończy się pomyślnie.  Jednak **Azure CDN from Akamai** nie obsługują profile **przeczyścić wszystkie**, więc jeśli profil Akamai zastosowaniu w tym samouczku, I potrzebny tooinclude toopurge określonej ścieżki.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Usuwanie punktów końcowych i profilów usługi CDN
metody ostatniego Hello usunie naszych punktu końcowego i profilu.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Uruchomiony program hello
Firma Microsoft może teraz skompilować i uruchomić hello program klikając hello **Start** przycisku w programie Visual Studio.

![Program uruchomiony](./media/cdn-app-dev-net/cdn-program-running-1.png)

Gdy hello program osiągnie hello powyżej wiersza, powinien być grupy zasobów tooyour stanie tooreturn w hello portalu Azure i zobacz hello profil został utworzony.

![Powodzenie!](./media/cdn-app-dev-net/cdn-success.png)

Potwierdzamy można następnie hello monity toorun hello reszty hello program.

![Kończenie pracy programu](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Następne kroki
Projekt ukończyć powitalnych toosee z tego przewodnika [pobieranie próbki hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

toofind dodatkową dokumentację hello biblioteki zarządzania usługi Azure CDN dla platformy .NET, widok hello [odwołania w witrynie MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).

