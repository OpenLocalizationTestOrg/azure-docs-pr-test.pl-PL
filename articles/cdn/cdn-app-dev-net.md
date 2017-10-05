---
title: "Rozpoczynanie pracy z biblioteki usługi Azure CDN dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pisać aplikacje .NET do zarządzania usługi Azure CDN przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="d8377-103">Rozpoczynanie pracy z wdrażaniem usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d8377-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8377-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="d8377-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="d8377-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d8377-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="d8377-106">Można użyć [biblioteki usługi Azure CDN dla platformy .NET](https://msdn.microsoft.com/library/mt657769.aspx) można zautomatyzować tworzenie i zarządzanie profilami sieci CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d8377-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="d8377-107">Ten samouczek przeprowadza przez tworzenie prostej aplikacji konsoli .NET, która przedstawia niektóre z dostępnych operacji.</span><span class="sxs-lookup"><span data-stu-id="d8377-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="d8377-108">W tym samouczku nie ma na celu opis wszystkich aspektów z biblioteki usługi Azure CDN dla platformy .NET szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="d8377-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="d8377-109">Potrzebujesz programu Visual Studio 2015 do ukończenia tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d8377-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="d8377-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) jest dostępny do pobrania.</span><span class="sxs-lookup"><span data-stu-id="d8377-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="d8377-111">[Ukończone projektu z tego samouczka](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) jest dostępny do pobrania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="d8377-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="d8377-112">Tworzenie projektu i dodawanie pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="d8377-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="d8377-113">Teraz, opracowaliśmy grupę zasobów dla naszych profilów CDN i naszych uprawnienia aplikacji usługi Azure AD do zarządzania profilami sieci CDN i punkty końcowe w ramach tej grupy, możemy rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8377-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="d8377-114">W programie Visual Studio 2015, kliknij **pliku**, **nowy**, **projektu...**  aby otworzyć okno dialogowe nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="d8377-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="d8377-115">Rozwiń węzeł **Visual C#**, a następnie wybierz pozycję **Windows** w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d8377-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="d8377-116">Kliknij przycisk **aplikacji konsoli** w środkowym okienku.</span><span class="sxs-lookup"><span data-stu-id="d8377-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="d8377-117">Nazwij swój projekt, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8377-117">Name your project, then click **OK**.</span></span>  

![Nowy projekt](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="d8377-119">Nasze projektu będzie korzystać z niektórych bibliotek Azure zawartych w pakietach Nuget.</span><span class="sxs-lookup"><span data-stu-id="d8377-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="d8377-120">Dodajmy tych do projektu.</span><span class="sxs-lookup"><span data-stu-id="d8377-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="d8377-121">Kliknij przycisk **narzędzia** menu **Menedżera pakietów Nuget**, następnie **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="d8377-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Zarządzaj pakietami Nuget](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="d8377-123">W konsoli Menedżera pakietów, wykonaj następujące polecenie, aby zainstalować **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="d8377-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="d8377-124">Wykonaj następujące czynności, aby zainstalować **biblioteki zarządzania usługi Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="d8377-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="d8377-125">Dyrektywy, Metoda główna, stałe i metody pomocnicze</span><span class="sxs-lookup"><span data-stu-id="d8377-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="d8377-126">Załóż podstawowej struktury nasz program zapisywane.</span><span class="sxs-lookup"><span data-stu-id="d8377-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="d8377-127">Wróć na karcie Program.cs Zastąp `using` dyrektywy u góry, z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d8377-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="d8377-128">Musimy zdefiniować niektóre stałe, używanego przez naszych metod.</span><span class="sxs-lookup"><span data-stu-id="d8377-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="d8377-129">W `Program` klasy, ale przed wysłaniem `Main` metody, Dodaj następujący kod.</span><span class="sxs-lookup"><span data-stu-id="d8377-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="d8377-130">Koniecznie Zastąp symbole zastępcze w tym  **&lt;nawiasy&gt;**, z własne wartości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d8377-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="d8377-131">Także zdefiniować te dwie zmienne na poziomie klasy.</span><span class="sxs-lookup"><span data-stu-id="d8377-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="d8377-132">Użyjemy tych później do określenia, czy naszych profilu i punktu końcowego już istnieje.</span><span class="sxs-lookup"><span data-stu-id="d8377-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="d8377-133">Zastąp `Main` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d8377-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="d8377-134">Niektóre z naszych innych metod mają być monit z pytaniami "Yes/No".</span><span class="sxs-lookup"><span data-stu-id="d8377-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="d8377-135">Dodaj następującą metodę, aby ułatwić który nieco:</span><span class="sxs-lookup"><span data-stu-id="d8377-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="d8377-136">Teraz, gdy podstawowa struktura nasz program napisano, powinien utworzyć metody wywoływane przez `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="d8377-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="d8377-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="d8377-137">Authentication</span></span>
<span data-ttu-id="d8377-138">Zanim możemy użyć biblioteki zarządzania usługi Azure CDN, musimy uwierzytelniania naszych nazwy głównej usługi i uzyskiwanie tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d8377-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="d8377-139">Ta metoda używa biblioteki ADAL do pobrania tokenu.</span><span class="sxs-lookup"><span data-stu-id="d8377-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="d8377-140">Jeśli używasz uwierzytelniania użytkownika `GetAccessToken` metody będą różnić się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="d8377-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8377-141">Ten przykładowy kod należy używać, tylko jeśli wybierzesz do uwierzytelniania indywidualnych użytkowników zamiast nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="d8377-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="d8377-142">Pamiętaj zastąpić `<redirect URI>` z przekierowania URI wprowadzona podczas rejestrowania aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8377-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8377-143">Lista profilów CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d8377-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="d8377-144">Teraz już wszystko gotowe do wykonywania operacji CDN.</span><span class="sxs-lookup"><span data-stu-id="d8377-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="d8377-145">Przede wszystkim naszym — metoda nie jest lista wszystkich profilów i punktów końcowych w naszej grupy zasobów, a w przypadku odnalezienia pasuje do nazwy profilu i punktu końcowego określona w naszym stałe odnotowuje tego na później, firma Microsoft nie należy próbować tworzyć duplikaty.</span><span class="sxs-lookup"><span data-stu-id="d8377-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8377-146">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d8377-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="d8377-147">Następnie utworzymy profilu.</span><span class="sxs-lookup"><span data-stu-id="d8377-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="d8377-148">Po utworzeniu profilu, utworzymy punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d8377-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="d8377-149">W powyższym przykładzie przypisuje punktu końcowego o nazwie początek *Contoso* z nazwą hosta `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d8377-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="d8377-150">Należy zmienić ten wskazywał hosta własne źródła.</span><span class="sxs-lookup"><span data-stu-id="d8377-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="d8377-151">Przeczyszczanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="d8377-151">Purge an endpoint</span></span>
<span data-ttu-id="d8377-152">Zakładając, że utworzono punkt końcowy, jeden typowe zadania, które firma Microsoft może być wykonanie w nasz program jest przeczyszczanie zawartości w naszym punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d8377-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="d8377-153">W przykładzie przedstawionym powyżej ciąg `/*` oznacza, że chcę przeczyścić wszystkie elementy w folderze głównym ścieżkę punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d8377-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="d8377-154">Jest to równoważne sprawdzanie **przeczyścić wszystkie** w oknie dialogowym "przeczyścić" w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d8377-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="d8377-155">W `CreateCdnProfile` metody, po utworzeniu profilu naszych jako **Azure CDN from Verizon** profilu, używając kodu `Sku = new Sku(SkuName.StandardVerizon)`, więc to zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d8377-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="d8377-156">Jednak **Azure CDN from Akamai** nie obsługują profile **przeczyścić wszystkie**, więc jeśli profil Akamai zastosowaniu w tym samouczku, I należy dołączyć określonej ścieżki do przeczyszczenia.</span><span class="sxs-lookup"><span data-stu-id="d8377-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8377-157">Usuwanie punktów końcowych i profilów usługi CDN</span><span class="sxs-lookup"><span data-stu-id="d8377-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="d8377-158">Ostatni metody usunie naszych punktu końcowego i profilu.</span><span class="sxs-lookup"><span data-stu-id="d8377-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="d8377-159">Uruchomienie programu</span><span class="sxs-lookup"><span data-stu-id="d8377-159">Running the program</span></span>
<span data-ttu-id="d8377-160">Firma Microsoft może teraz skompilować i uruchomić program klikając **Start** przycisku w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8377-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Program uruchomiony](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="d8377-162">Gdy program osiągnie wiersz powyżej, można powrócić do tej grupy zasobów w portalu Azure i zobaczyć, czy profil został utworzony.</span><span class="sxs-lookup"><span data-stu-id="d8377-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Powodzenie!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="d8377-164">Następnie można potwierdzamy z monitami, aby uruchomić całego programu.</span><span class="sxs-lookup"><span data-stu-id="d8377-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Kończenie pracy programu](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="d8377-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8377-166">Next Steps</span></span>
<span data-ttu-id="d8377-167">Aby wyświetlić ukończone projektu z tego przewodnika [Pobierz przykład](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="d8377-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="d8377-168">Aby uzyskać dodatkową dokumentację z biblioteki usługi Azure CDN zarządzania dla platformy .NET, Wyświetl [odwołania w witrynie MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8377-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="d8377-169">Zarządzanie zasobami CDN za pomocą [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d8377-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

