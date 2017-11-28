---
title: "aaaUsing tooaccess zestawu .NET SDK usługi Azure Mobile Engagement usługi API"
description: "W tym artykule opisano, jak toouse hello tooaccess zestaw .NET SDK usługi Mobile Engagement interfejsów API usługi Azure Mobile Engagement usługi"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="4b032-103">Przy użyciu zestawu .NET SDK tooaccess interfejsów API usługi Azure Mobile Engagement usługi</span><span class="sxs-lookup"><span data-stu-id="4b032-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="4b032-104">Usługa Azure Mobile Engagement udostępnia zestaw interfejsów API dla Ciebie urządzeń toomanage, Reach lub wypchnąć kampanie, itp. toointeract z poniższych interfejsów API, firma Microsoft udostępnia również możesz [plik struktury Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) korzystając z narzędzi zestawów SDK toogenerate dla preferowany język.</span><span class="sxs-lookup"><span data-stu-id="4b032-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="4b032-105">Firma Microsoft zaleca używanie hello [AutoRest](https://github.com/Azure/AutoRest) narzędzia toogenerate zestawu SDK z naszych pliku programu Swagger.</span><span class="sxs-lookup"><span data-stu-id="4b032-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="4b032-106">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="4b032-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="4b032-107">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="4b032-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="4b032-108">Zestaw .NET SDK został utworzony w podobny sposób, co pozwala toointeract z poniższych interfejsów API przy użyciu otoki C# i nie ma toodo hello negocjacji token uwierzytelniania, a następnie Odśwież samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="4b032-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="4b032-109">W tym przykładzie przechodzi przez zestaw hello kroki toofollow toouse hello zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="4b032-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="4b032-110">Przede wszystkim należy toosetup hello uwierzytelniania dla swoje interfejsy API przy użyciu hello Azure Active Directory zgodnie z opisem [tutaj](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="4b032-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="4b032-111">Na końcu hello tych kroków, powinien mieć prawidłową **SubscriptionId**, **TenantId**, **ApplicationId** i **klucz tajny**.</span><span class="sxs-lookup"><span data-stu-id="4b032-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="4b032-112">Używamy proste toodemonstrate aplikacji konsoli systemu Windows, Praca z hello zestawu .NET SDK ze scenariuszem hello tworzenie kampanii anonsu.</span><span class="sxs-lookup"><span data-stu-id="4b032-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="4b032-113">Sposób otwarcia programu Visual Studio i utworzyć **aplikacji konsoli**.</span><span class="sxs-lookup"><span data-stu-id="4b032-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="4b032-114">Następnie muszą hello toodownload zestawu .NET SDK, który jest dostępny jako **Biblioteka zarządzania Microsoft Azure Engagement** w galerii Nuget hello [tutaj](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="4b032-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="4b032-115">Jeśli instalujesz hello Nuget w programie Visual Studio, należy tooensure, że masz wyboru oznaczone hello **Uwzględnij wersję wstępną** opcja podczas wyszukiwania dla pakietu hello:</span><span class="sxs-lookup"><span data-stu-id="4b032-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="4b032-116">W hello `Program.cs` plików, Dodaj następujące obszary nazw hello:</span><span class="sxs-lookup"><span data-stu-id="4b032-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="4b032-117">Następnie należy hello toodefine po stałe, które będą używane do uwierzytelniania i interakcji z hello Mobile Engagement App, w którym tworzysz hello anonsu kampanii:</span><span class="sxs-lookup"><span data-stu-id="4b032-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="4b032-118">Zdefiniuj hello `EngagementManagementClient` zmienną, w której używamy toocall hello zestaw SDK usługi Mobile Engagement metod:</span><span class="sxs-lookup"><span data-stu-id="4b032-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="4b032-119">Dodaj następujące tooyour hello `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="4b032-119">Add hello following tooyour `Main` method:</span></span>
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="4b032-120">Zdefiniuj powitania po metodę, która zajmuje się inicjowanie hello `EngagementManagementClient` najpierw uwierzytelniania i kojarzenie sam z hello Mobile Engagement App, w którym planujesz toocreate hello anonsu kampanii:</span><span class="sxs-lookup"><span data-stu-id="4b032-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="4b032-121">Należy pamiętać, że należy toouse hello **nazwa zasobów aplikacji** zgodnie z definicją w portalu zarządzania Azure hello hello AppName parametru.</span><span class="sxs-lookup"><span data-stu-id="4b032-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="4b032-122">Ponadto zdefiniować metody CreateCampaign hello, który zajmie się przy użyciu toocreate EngagementClient hello poprzednio inicjowany prostą **w każdej chwili** & **tylko powiadomienia** kampanii Tytuł i komunikat:</span><span class="sxs-lookup"><span data-stu-id="4b032-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="4b032-123">Hello wykonywania aplikacji konsoli, a, zostanie wyświetlony następujący hello pomyślnym utworzeniu kampanii hello:</span><span class="sxs-lookup"><span data-stu-id="4b032-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="4b032-124">**Identyfikator kampanii "159" został pomyślnie utworzony i jest w stanie "Projekt"**</span><span class="sxs-lookup"><span data-stu-id="4b032-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
