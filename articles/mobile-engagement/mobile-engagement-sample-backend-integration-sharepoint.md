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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement — Integracja z interfejsem API
W systemie marketing automatyczne tworzenie i aktywowanie hello kampanii marketingowych, również są wykonywane automatycznie. W tym celu — usługi Azure Mobile Engagement umożliwia tworzenie takich automatycznych kampanii marketingowych, jak również za pomocą interfejsów API. 

Zwykle używać hello Mobile Engagement fronton interfejsu toocreate anonsów/sond itp jako część ich kampanii marketingowych. Jednak jako hello stają się dojrzałe kampanii marketingowych, konieczne jest tooleverage hello danych zablokowane hello systemów wewnętrznej bazy danych (na przykład systemu CRM lub system CMS, takich jak SharePoint), aby w pełni zautomatyzowanego procesu mogą być tworzone, co powoduje kampanii w Mobile Dynamicznie na podstawie hello danych przesyłane w od systemów zaplecza hello zaangażowania. 

![][5]

Ten samouczek zbliża się do takiej sytuacji, gdy użytkownik biznesowych programu SharePoint wypełnia listę programu SharePoint przy użyciu danych marketingowych i zautomatyzowany proces przejmuje elementy z listy hello i nawiązanie połączenia z hello Mobile Engagement systemu za pomocą hello dostępne interfejsów API REST toocreate kampanię marketingową z hello danych programu SharePoint. 

> [!IMPORTANT]
> Ogólnie rzecz biorąc można użyć tego przykładu jako punktu wyjścia do zrozumienia, jak toocall żadnych Mobile Engagement interfejsu API REST ponieważ szczegóły hello dwa kluczowe aspekty wywoływania hello interfejsów API - parametry uwierzytelniania i przechodzącą. 
> 
> 

## <a name="sharepoint-integration"></a>Integracja z programem SharePoint
1. Oto przykładowe jakie hello wygląda listy programu SharePoint. **Tytuł**, **kategorii**, **NotificationTitle**, **komunikat** i **adres URL** są używane do tworzenia hello anonsu. Brak kolumnę o nazwie **IsProcessed** używany przez proces automatyzacji próbki hello w postaci hello konsoli programu. Możesz uruchomić ten program konsoli jako zadanie WebJob platformy Azure, aby można ją zaplanować lub bezpośrednio umożliwia tworzenie tooprogram przepływu pracy programu SharePoint hello i aktywowanie anonsu powitania po wstawieniu elementu do listy programu SharePoint hello. W tym przykładzie używamy hello konsoli programu, który przechodzi między elementami hello w hello SharePoint listy i utworzyć anons w usłudze Azure Mobile Engagement dla każdej z nich, a następnie oznacza koniec hello **IsProcessed** flagi toobe true na utworzenie anonsu powiodło się.
   
    ![][1]
2. Używamy hello kodu z próbki hello *zdalnego uwierzytelniania w hello SharePoint Online przy użyciu Client Object Model* [tutaj](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate z hello listy programu SharePoint.
3. Po uwierzytelnieniu pętla za pośrednictwem hello listy elementów toofind nowo utworzony elementów (będą mieć **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Integracja usługi Mobile Engagement
1. Po znaleźliśmy elementu, który wymaga przetwarzania — możemy wyodrębnić wymaganych informacji hello toocreate anonsu z hello elementu listy, a następnie wywołać `CreateAzMECampaign` toocreate go, a następnie `ActivateAzMECampaign` tooactivate go. Są to zasadniczo wywołania interfejsu API REST wywoływania toohello zapleczem usługi Mobile Engagement. 
2. Witaj interfejsów API REST usługi Engagement Mobile wymagają **nagłówek autoryzacji HTTP schemat uwierzytelniania podstawowego** który składa się z hello `ApplicationId` i hello `ApiKey` uzyskane z portalu Azure hello. Upewnij się, że używasz hello klucza z hello **klucze interfejsu api** sekcji i *nie* z hello **klucze sdk** sekcji. 
   
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
3. Do tworzenia hello anonsu typu kampanii - zajrzyj toohello [dokumentacji](https://msdn.microsoft.com/library/azure/mt683750.aspx). Należy się, że określasz kampanii hello toomake `kind` jako *anonsu* i hello [ładunku](https://msdn.microsoft.com/library/azure/mt683751.aspx) i przekazaniem go jako FormUrlEncodedContent. 
   
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
4. Po utworzeniu anonsu hello utworzone, zobaczysz przypominać hello na portalu Mobile Engagement hello (należy pamiętać, że hello stan = roboczą i Activated = Brak)
   
    ![][3]
5. `CreateAzMECampaign`Tworzy kampanii anons i zwraca jego identyfikator toohello wywołującego. `ActivateAzMECampaign`wymaga to identyfikator jako hello parametru tooactivate hello kampanii. 
   
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
6. Po utworzeniu anonsu hello aktywowany, zostanie wyświetlony przypominać następujące hello w portalu Mobile Engagement hello:
   
    ![][4]
7. Jak aktywować pobiera kampanii hello, wszystkie urządzenia, które spełniają kryterium hello na powitania kampanii rozpocznie się wyświetlać powiadomienia. 
8. Również zauważysz oznaczony element listy hello IsProcessed = false ustawiono tooTrue po utworzeniu hello anonsu kampanii.  

W tym przykładzie tworzone kampanii proste anonsu określania przede wszystkim hello wymagane właściwości. To ustawienie można dostosować jak mogą z portalu hello przy użyciu informacji hello [tutaj](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



