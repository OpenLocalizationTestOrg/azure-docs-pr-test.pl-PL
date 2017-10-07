---
title: "aaaAzure Mobile Engagement — integracja wewnętrznej bazy danych"
description: "Łączenie usługi Azure Mobile Engagement z kampaniami toocreate wewnętrznej bazy danych programu SharePoint, z programu SharePoint"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="3b222-103">Azure Mobile Engagement — Integracja z interfejsem API</span><span class="sxs-lookup"><span data-stu-id="3b222-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="3b222-104">W systemie marketing automatyczne tworzenie i aktywowanie hello kampanii marketingowych, również są wykonywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3b222-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="3b222-105">W tym celu — usługi Azure Mobile Engagement umożliwia tworzenie takich automatycznych kampanii marketingowych, jak również za pomocą interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3b222-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="3b222-106">Zwykle używać hello Mobile Engagement fronton interfejsu toocreate anonsów/sond itp jako część ich kampanii marketingowych.</span><span class="sxs-lookup"><span data-stu-id="3b222-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="3b222-107">Jednak jako hello stają się dojrzałe kampanii marketingowych, konieczne jest tooleverage hello danych zablokowane hello systemów wewnętrznej bazy danych (na przykład systemu CRM lub system CMS, takich jak SharePoint), aby w pełni zautomatyzowanego procesu mogą być tworzone, co powoduje kampanii w Mobile Dynamicznie na podstawie hello danych przesyłane w od systemów zaplecza hello zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="3b222-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="3b222-108">Ten samouczek zbliża się do takiej sytuacji, gdy użytkownik biznesowych programu SharePoint wypełnia listę programu SharePoint przy użyciu danych marketingowych i zautomatyzowany proces przejmuje elementy z listy hello i nawiązanie połączenia z hello Mobile Engagement systemu za pomocą hello dostępne interfejsów API REST toocreate kampanię marketingową z hello danych programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3b222-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3b222-109">Ogólnie rzecz biorąc można użyć tego przykładu jako punktu wyjścia do zrozumienia, jak toocall żadnych Mobile Engagement interfejsu API REST ponieważ szczegóły hello dwa kluczowe aspekty wywoływania hello interfejsów API - parametry uwierzytelniania i przechodzącą.</span><span class="sxs-lookup"><span data-stu-id="3b222-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="3b222-110">Integracja z programem SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b222-110">SharePoint integration</span></span>
1. <span data-ttu-id="3b222-111">Oto przykładowe jakie hello wygląda listy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3b222-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="3b222-112">**Tytuł**, **kategorii**, **NotificationTitle**, **komunikat** i **adres URL** są używane do tworzenia hello anonsu.</span><span class="sxs-lookup"><span data-stu-id="3b222-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="3b222-113">Brak kolumnę o nazwie **IsProcessed** używany przez proces automatyzacji próbki hello w postaci hello konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="3b222-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="3b222-114">Możesz uruchomić ten program konsoli jako zadanie WebJob platformy Azure, aby można ją zaplanować lub bezpośrednio umożliwia tworzenie tooprogram przepływu pracy programu SharePoint hello i aktywowanie anonsu powitania po wstawieniu elementu do listy programu SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="3b222-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="3b222-115">W tym przykładzie używamy hello konsoli programu, który przechodzi między elementami hello w hello SharePoint listy i utworzyć anons w usłudze Azure Mobile Engagement dla każdej z nich, a następnie oznacza koniec hello **IsProcessed** flagi toobe true na utworzenie anonsu powiodło się.</span><span class="sxs-lookup"><span data-stu-id="3b222-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="3b222-116">Używamy hello kodu z próbki hello *zdalnego uwierzytelniania w hello SharePoint Online przy użyciu Client Object Model* [tutaj](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate z hello listy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3b222-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="3b222-117">Po uwierzytelnieniu pętla za pośrednictwem hello listy elementów toofind nowo utworzony elementów (będą mieć **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="3b222-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="3b222-118">Integracja usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3b222-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="3b222-119">Po znaleźliśmy elementu, który wymaga przetwarzania — możemy wyodrębnić wymaganych informacji hello toocreate anonsu z hello elementu listy, a następnie wywołać `CreateAzMECampaign` toocreate go, a następnie `ActivateAzMECampaign` tooactivate go.</span><span class="sxs-lookup"><span data-stu-id="3b222-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="3b222-120">Są to zasadniczo wywołania interfejsu API REST wywoływania toohello zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3b222-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="3b222-121">Witaj interfejsów API REST usługi Engagement Mobile wymagają **nagłówek autoryzacji HTTP schemat uwierzytelniania podstawowego** który składa się z hello `ApplicationId` i hello `ApiKey` uzyskane z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3b222-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="3b222-122">Upewnij się, że używasz hello klucza z hello **klucze interfejsu api** sekcji i *nie* z hello **klucze sdk** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3b222-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="3b222-123">Do tworzenia hello anonsu typu kampanii - zajrzyj toohello [dokumentacji](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b222-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="3b222-124">Należy się, że określasz kampanii hello toomake `kind` jako *anonsu* i hello [ładunku](https://msdn.microsoft.com/library/azure/mt683751.aspx) i przekazaniem go jako FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="3b222-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="3b222-125">Po utworzeniu anonsu hello utworzone, zobaczysz przypominać hello na portalu Mobile Engagement hello (należy pamiętać, że hello stan = roboczą i Activated = Brak)</span><span class="sxs-lookup"><span data-stu-id="3b222-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="3b222-126">`CreateAzMECampaign`Tworzy kampanii anons i zwraca jego identyfikator toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="3b222-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="3b222-127">`ActivateAzMECampaign`wymaga to identyfikator jako hello parametru tooactivate hello kampanii.</span><span class="sxs-lookup"><span data-stu-id="3b222-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="3b222-128">Po utworzeniu anonsu hello aktywowany, zostanie wyświetlony przypominać następujące hello w portalu Mobile Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="3b222-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="3b222-129">Jak aktywować pobiera kampanii hello, wszystkie urządzenia, które spełniają kryterium hello na powitania kampanii rozpocznie się wyświetlać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3b222-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="3b222-130">Również zauważysz oznaczony element listy hello IsProcessed = false ustawiono tooTrue po utworzeniu hello anonsu kampanii.</span><span class="sxs-lookup"><span data-stu-id="3b222-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="3b222-131">W tym przykładzie tworzone kampanii proste anonsu określania przede wszystkim hello wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="3b222-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="3b222-132">To ustawienie można dostosować jak mogą z portalu hello przy użyciu informacji hello [tutaj](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b222-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



