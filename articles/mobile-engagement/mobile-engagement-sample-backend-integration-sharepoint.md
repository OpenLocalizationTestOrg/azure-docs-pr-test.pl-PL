---
title: "Azure Mobile Engagement — integracja wewnętrznej bazy danych"
description: "Łączenie usługi Azure Mobile Engagement z zapleczem programu SharePoint, aby utworzyć kampanie z programu SharePoint"
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
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="12d77-103">Azure Mobile Engagement — Integracja z interfejsem API</span><span class="sxs-lookup"><span data-stu-id="12d77-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="12d77-104">W systemie marketing automatyczne tworzenie i aktywowanie kampanii marketingowych również automatycznie są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="12d77-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="12d77-105">W tym celu — usługi Azure Mobile Engagement umożliwia tworzenie takich automatycznych kampanii marketingowych, jak również za pomocą interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="12d77-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="12d77-106">Zwykle klientów umożliwia utworzenie anonsów/sond itp jako część ich kampanii marketingowych interfejs frontonu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="12d77-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="12d77-107">Jednak ponieważ dojrzałe zaczynają kampanii marketingowych, istnieje potrzeba wykorzystanie danych zablokowane w systemach wewnętrznej bazy danych (na przykład systemu CRM lub system CMS, takich jak SharePoint), aby w pełni zautomatyzowanego procesu mogą być tworzone, co powoduje kampanii w dynamicznie na podstawie danych przesyłane w od systemów zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="12d77-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="12d77-108">W tym samouczku przechodzi przez takiej sytuacji, gdy użytkowników biznesowych programu SharePoint wypełnia listę programu SharePoint przy użyciu danych marketingowych i zautomatyzowany proces przejmuje elementów na liście i łączy się z systemu Mobile Engagement przy użyciu dostępnych interfejsach API REST, aby utworzyć kampanię marketingową na podstawie danych programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12d77-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="12d77-109">Ogólnie rzecz biorąc można użyć tego przykładu jako punktu wyjścia do zrozumieć, jak wywołać interfejsu API REST żadnych Mobile Engagement, jak szczegółowe informacje dotyczące wywoływania interfejsów API - parametry uwierzytelniania i przechodzącą dwa kluczowe aspekty.</span><span class="sxs-lookup"><span data-stu-id="12d77-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="12d77-110">Integracja z programem SharePoint</span><span class="sxs-lookup"><span data-stu-id="12d77-110">SharePoint integration</span></span>
1. <span data-ttu-id="12d77-111">Oto, jak wygląda przykładową listę programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12d77-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="12d77-112">**Tytuł**, **kategorii**, **NotificationTitle**, **komunikat** i **adres URL** są używane do tworzenia anonsu.</span><span class="sxs-lookup"><span data-stu-id="12d77-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="12d77-113">Brak kolumnę o nazwie **IsProcessed** używany przez proces automatyzacji próbki w formie program konsoli.</span><span class="sxs-lookup"><span data-stu-id="12d77-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="12d77-114">Można uruchomić tej konsoli programu jako zadanie WebJob platformy Azure, dzięki czemu można zaplanować lub możesz bezpośrednio użyć przepływu pracy programu SharePoint do programu, tworzenia i aktywowanie powiadomienia po wstawieniu elementu do listy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12d77-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="12d77-115">W tym przykładzie używamy programu konsoli, który przechodzi przez elementy programu SharePoint listy i utworzyć anons w usłudze Azure Mobile Engagement dla każdej z nich, a następnie oznacza koniec **IsProcessed** flagi spełniony przy tworzeniu anonsu powiodło się.</span><span class="sxs-lookup"><span data-stu-id="12d77-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="12d77-116">Używamy kodu z próbki *uwierzytelniania zdalnego w programie SharePoint Online przy użyciu Client Object Model* [tutaj](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) do uwierzytelniania za pomocą listy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12d77-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="12d77-117">Po uwierzytelnieniu pętla za pomocą elementów listy, aby dowiedzieć się, wszystkie nowo utworzone elementy (będą mieć **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="12d77-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="12d77-118">Integracja usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="12d77-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="12d77-119">Po znaleźliśmy elementu, który wymaga przetwarzania — możemy wyodrębnić informacje wymagane do tworzenia anonsu z elementu listy, a wywołania `CreateAzMECampaign` go utworzyć, a następnie `ActivateAzMECampaign` aby aktywować go.</span><span class="sxs-lookup"><span data-stu-id="12d77-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="12d77-120">Są to zasadniczo wywołania interfejsu API REST wywoływanie z zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="12d77-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="12d77-121">Wymagaj interfejsów API REST Mobile Engagement **nagłówek autoryzacji HTTP schemat uwierzytelniania podstawowego** który składa się z `ApplicationId` i `ApiKey` uzyskane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="12d77-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="12d77-122">Upewnij się, że używasz klucza z **klucze interfejsu api** sekcji i *nie* z **klucze sdk** sekcji.</span><span class="sxs-lookup"><span data-stu-id="12d77-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="12d77-123">Do tworzenia anonsu typu kampanii - zajrzyj do [dokumentacji](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="12d77-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="12d77-124">Należy się upewnić, że określasz kampanii `kind` jako *anonsu* i [ładunku](https://msdn.microsoft.com/library/azure/mt683751.aspx) i przekazaniem go jako FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="12d77-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
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
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
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
4. <span data-ttu-id="12d77-125">Po utworzeniu, aby utworzyć anons, zobaczysz ekran podobny do następujących w portalu Mobile Engagement (należy pamiętać, że stan = roboczą i Activated = Brak)</span><span class="sxs-lookup"><span data-stu-id="12d77-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="12d77-126">`CreateAzMECampaign`Tworzy kampanii anons i zwraca jego identyfikator do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="12d77-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="12d77-127">`ActivateAzMECampaign`wymaga to identyfikator jako parametru, aby aktywować kampanię.</span><span class="sxs-lookup"><span data-stu-id="12d77-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
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
   
                // Send the POST request
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
6. <span data-ttu-id="12d77-128">Po utworzeniu anons aktywowany, zostanie wyświetlony przypominać następujące w portalu Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="12d77-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="12d77-129">Jak aktywować pobiera kampanii, wszystkie urządzenia, które spełniają kryterium kampanii rozpocznie się wyświetlać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="12d77-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="12d77-130">Będzie także zauważyć, że element listy oznaczonych IsProcessed = false została ustawiona na wartość True po utworzeniu kampanii anonsu.</span><span class="sxs-lookup"><span data-stu-id="12d77-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="12d77-131">W tym przykładzie tworzone kampanii proste anonsu określania najczęściej wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="12d77-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="12d77-132">To ustawienie można dostosować zgodnie z potrzebami, korzystając z informacji w portalu można [tutaj](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="12d77-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



