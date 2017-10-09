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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="b6769-103">Rozpoczynanie pracy z wdrażaniem usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b6769-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6769-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6769-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="b6769-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b6769-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="b6769-106">Można użyć hello [biblioteki usługi Azure CDN dla platformy .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="b6769-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="b6769-107">Ten samouczek przeprowadzi Cię przez hello tworzenia prostej aplikacji konsoli .NET, która przedstawia niektóre z dostępnych operacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6769-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="b6769-108">Ten samouczek jest przeznaczony toodescribe wszystkich aspektów hello biblioteki usługi Azure CDN dla platformy .NET szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="b6769-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="b6769-109">Należy toocomplete programu Visual Studio 2015 w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b6769-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="b6769-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) jest dostępny do pobrania.</span><span class="sxs-lookup"><span data-stu-id="b6769-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="b6769-111">Witaj [ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) jest dostępny do pobrania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="b6769-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="b6769-112">Tworzenie projektu i dodawanie pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="b6769-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="b6769-113">Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych profilów usługi CDN toomanage uprawnienia aplikacji usługi Azure AD i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6769-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="b6769-114">W programie Visual Studio 2015, kliknij **pliku**, **nowy**, **projektu...**  tooopen powitalne okno dialogowe nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="b6769-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="b6769-115">Rozwiń węzeł **Visual C#**, a następnie wybierz pozycję **Windows** hello okienka po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="b6769-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="b6769-116">Kliknij przycisk **aplikacji konsoli** w okienku Centrum hello.</span><span class="sxs-lookup"><span data-stu-id="b6769-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="b6769-117">Nazwij swój projekt, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6769-117">Name your project, then click **OK**.</span></span>  

![Nowy projekt](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="b6769-119">Nasze projektu będzie toouse niektóre biblioteki Azure zawartych w pakietach Nuget.</span><span class="sxs-lookup"><span data-stu-id="b6769-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="b6769-120">Umożliwia dodanie tych toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="b6769-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="b6769-121">Kliknij przycisk hello **narzędzia** menu **Menedżera pakietów Nuget**, następnie **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="b6769-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Zarządzaj pakietami Nuget](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="b6769-123">W konsoli Menedżera pakietów hello, wykonaj następujące polecenie tooinstall hello hello **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="b6769-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="b6769-124">Wykonaj następujące tooinstall hello hello **biblioteki zarządzania usługi Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="b6769-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="b6769-125">Dyrektywy, Metoda główna, stałe i metody pomocnicze</span><span class="sxs-lookup"><span data-stu-id="b6769-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="b6769-126">Załóż hello podstawowej struktury nasz program zapisywane.</span><span class="sxs-lookup"><span data-stu-id="b6769-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="b6769-127">Powrót na karcie Program.cs hello, Zastąp hello `using` dyrektywy u góry hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b6769-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="b6769-128">Potrzebujemy toodefine niektóre stałe, używanego przez naszych metod.</span><span class="sxs-lookup"><span data-stu-id="b6769-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="b6769-129">W hello `Program` klasy, ale przed hello `Main` metody, Dodaj następujące hello.</span><span class="sxs-lookup"><span data-stu-id="b6769-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="b6769-130">Należy się tooreplace symbole zastępcze hello, w tym hello  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b6769-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="b6769-131">Również na poziomie klasy hello, należy zdefiniować te dwie zmienne.</span><span class="sxs-lookup"><span data-stu-id="b6769-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="b6769-132">Użyjemy tych toodetermine nowszych Jeśli naszych profilu i punktu końcowego już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b6769-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="b6769-133">Zastąp hello `Main` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b6769-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="b6769-134">Niektóre z naszych innych metod będzie tooprompt hello użytkownika za pomocą pytań "Yes/No".</span><span class="sxs-lookup"><span data-stu-id="b6769-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="b6769-135">Dodaj następujące metody toomake hello który nieco łatwiejsze:</span><span class="sxs-lookup"><span data-stu-id="b6769-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="b6769-136">Teraz, gdy podstawowa struktura nasz program hello są zapisywane, utworzymy powinien hello metody wywoływane przez hello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="b6769-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="b6769-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="b6769-137">Authentication</span></span>
<span data-ttu-id="b6769-138">Przed możemy użyć hello biblioteki zarządzania usługi Azure CDN, możemy muszą tooauthenticate nasza usługa główna i uzyskiwanie tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b6769-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="b6769-139">Ta metoda używa biblioteki ADAL tooretrieve hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="b6769-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="b6769-140">Jeśli używasz uwierzytelniania użytkownika hello `GetAccessToken` metody będą różnić się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="b6769-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6769-141">Ten przykładowy kod należy używać tylko, jeśli użytkownik zdecyduje toohave uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="b6769-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="b6769-142">Należy się tooreplace `<redirect URI>` z hello przekierowania URI wprowadzona podczas rejestrowania aplikacji hello w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6769-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="b6769-143">Lista profilów CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="b6769-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="b6769-144">Jest teraz gotowy tooperform operacji CDN.</span><span class="sxs-lookup"><span data-stu-id="b6769-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="b6769-145">Hello przede wszystkim naszym metoda wykonuje jest lista wszystkich profilów hello i punktów końcowych w naszej grupy zasobów, a w przypadku odnalezienia pasuje do nazwy profilu i punktu końcowego hello określone w naszym stałe udziela Uwaga tego na później, firma Microsoft nie próbuj toocreate duplikaty.</span><span class="sxs-lookup"><span data-stu-id="b6769-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="b6769-146">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="b6769-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="b6769-147">Następnie utworzymy profilu.</span><span class="sxs-lookup"><span data-stu-id="b6769-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="b6769-148">Po utworzeniu profilu hello utworzymy punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b6769-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="b6769-149">w powyższym przykładzie Hello przypisuje punktu końcowego hello pochodzenia o nazwie *Contoso* z nazwą hosta `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b6769-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="b6769-150">Należy zmienić nazwę hosta tego toopoint tooyour własnych źródła.</span><span class="sxs-lookup"><span data-stu-id="b6769-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="b6769-151">Przeczyszczanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="b6769-151">Purge an endpoint</span></span>
<span data-ttu-id="b6769-152">Przy założeniu, że utworzono punkt końcowy hello, jednego z typowych zadań, że firma Microsoft może być tooperform w naszym program jest przeczyszczanie hello zawartości w naszym punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b6769-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="b6769-153">W powyższym przykładzie hello, hello ciąg `/*` oznacza, że ma być toopurge wszystko w głównym hello hello ścieżkę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b6769-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="b6769-154">Jest to równoważne toochecking **przeczyścić wszystkie** w hello portalu Azure "przeczyścić" okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6769-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="b6769-155">W hello `CreateCdnProfile` metody, po utworzeniu profilu naszych jako **Azure CDN from Verizon** profilu przy użyciu kodu hello `Sku = new Sku(SkuName.StandardVerizon)`, więc to zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b6769-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="b6769-156">Jednak **Azure CDN from Akamai** nie obsługują profile **przeczyścić wszystkie**, więc jeśli profil Akamai zastosowaniu w tym samouczku, I potrzebny tooinclude toopurge określonej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b6769-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="b6769-157">Usuwanie punktów końcowych i profilów usługi CDN</span><span class="sxs-lookup"><span data-stu-id="b6769-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="b6769-158">metody ostatniego Hello usunie naszych punktu końcowego i profilu.</span><span class="sxs-lookup"><span data-stu-id="b6769-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="b6769-159">Uruchomiony program hello</span><span class="sxs-lookup"><span data-stu-id="b6769-159">Running hello program</span></span>
<span data-ttu-id="b6769-160">Firma Microsoft może teraz skompilować i uruchomić hello program klikając hello **Start** przycisku w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6769-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Program uruchomiony](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="b6769-162">Gdy hello program osiągnie hello powyżej wiersza, powinien być grupy zasobów tooyour stanie tooreturn w hello portalu Azure i zobacz hello profil został utworzony.</span><span class="sxs-lookup"><span data-stu-id="b6769-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Powodzenie!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="b6769-164">Potwierdzamy można następnie hello monity toorun hello reszty hello program.</span><span class="sxs-lookup"><span data-stu-id="b6769-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Kończenie pracy programu](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="b6769-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6769-166">Next Steps</span></span>
<span data-ttu-id="b6769-167">Projekt ukończyć powitalnych toosee z tego przewodnika [pobieranie próbki hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="b6769-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="b6769-168">toofind dodatkową dokumentację hello biblioteki zarządzania usługi Azure CDN dla platformy .NET, widok hello [odwołania w witrynie MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6769-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="b6769-169">Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b6769-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

