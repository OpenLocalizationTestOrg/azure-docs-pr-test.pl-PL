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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>Przy użyciu zestawu .NET SDK tooaccess interfejsów API usługi Azure Mobile Engagement usługi
Usługa Azure Mobile Engagement udostępnia zestaw interfejsów API dla Ciebie urządzeń toomanage, Reach lub wypchnąć kampanie, itp. toointeract z poniższych interfejsów API, firma Microsoft udostępnia również możesz [plik struktury Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) korzystając z narzędzi zestawów SDK toogenerate dla preferowany język. Firma Microsoft zaleca używanie hello [AutoRest](https://github.com/Azure/AutoRest) narzędzia toogenerate zestawu SDK z naszych pliku programu Swagger.

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Zestaw .NET SDK został utworzony w podobny sposób, co pozwala toointeract z poniższych interfejsów API przy użyciu otoki C# i nie ma toodo hello negocjacji token uwierzytelniania, a następnie Odśwież samodzielnie.  

W tym przykładzie przechodzi przez zestaw hello kroki toofollow toouse hello zestawu .NET SDK:

1. Przede wszystkim należy toosetup hello uwierzytelniania dla swoje interfejsy API przy użyciu hello Azure Active Directory zgodnie z opisem [tutaj](mobile-engagement-api-authentication.md#authentication). Na końcu hello tych kroków, powinien mieć prawidłową **SubscriptionId**, **TenantId**, **ApplicationId** i **klucz tajny**. 
2. Używamy proste toodemonstrate aplikacji konsoli systemu Windows, Praca z hello zestawu .NET SDK ze scenariuszem hello tworzenie kampanii anonsu. Sposób otwarcia programu Visual Studio i utworzyć **aplikacji konsoli**.   
3. Następnie muszą hello toodownload zestawu .NET SDK, który jest dostępny jako **Biblioteka zarządzania Microsoft Azure Engagement** w galerii Nuget hello [tutaj](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Jeśli instalujesz hello Nuget w programie Visual Studio, należy tooensure, że masz wyboru oznaczone hello **Uwzględnij wersję wstępną** opcja podczas wyszukiwania dla pakietu hello:
   
    ![][1]
4. W hello `Program.cs` plików, Dodaj następujące obszary nazw hello:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Następnie należy hello toodefine po stałe, które będą używane do uwierzytelniania i interakcji z hello Mobile Engagement App, w którym tworzysz hello anonsu kampanii:
   
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
6. Zdefiniuj hello `EngagementManagementClient` zmienną, w której używamy toocall hello zestaw SDK usługi Mobile Engagement metod:
   
        static EngagementManagementClient engagementClient; 
7. Dodaj następujące tooyour hello `Main` metody:
   
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
8. Zdefiniuj powitania po metodę, która zajmuje się inicjowanie hello `EngagementManagementClient` najpierw uwierzytelniania i kojarzenie sam z hello Mobile Engagement App, w którym planujesz toocreate hello anonsu kampanii:
   
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
   > Należy pamiętać, że należy toouse hello **nazwa zasobów aplikacji** zgodnie z definicją w portalu zarządzania Azure hello hello AppName parametru. 
   > 
   > 
9. Ponadto zdefiniować metody CreateCampaign hello, który zajmie się przy użyciu toocreate EngagementClient hello poprzednio inicjowany prostą **w każdej chwili** & **tylko powiadomienia** kampanii Tytuł i komunikat: 
   
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
10. Hello wykonywania aplikacji konsoli, a, zostanie wyświetlony następujący hello pomyślnym utworzeniu kampanii hello:
    
    **Identyfikator kampanii "159" został pomyślnie utworzony i jest w stanie "Projekt"**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
