---
title: "Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service (GoDaddy)"
description: "Dowiedz się, jak użyć nazwy domeny z GoDaddy dla aplikacji sieci Web Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="06e28-103">Konfigurowanie nazwy domeny niestandardowej (kupionej bezpośrednio od firmy GoDaddy) w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="06e28-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="06e28-104">Jeśli została kupione domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure odwoływać się do ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="06e28-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="06e28-105">Ten artykuł zawiera instrukcje przy użyciu nazwy domeny niestandardowej, które zostało zakupione bezpośrednio z [GoDaddy](https://godaddy.com) z [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="06e28-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="06e28-106">Opis rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="06e28-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="06e28-107">Dodaj rekord DNS dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="06e28-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="06e28-108">Aby skojarzyć domeny niestandardowej z aplikacją sieci web w usłudze App Service, możesz należy dodać nowy wpis w tabeli DNS dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="06e28-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="06e28-109">Wykonaj następujące kroki, aby zlokalizować narzędzia DNS dla GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="06e28-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="06e28-110">Zaloguj się na swoje konto w GoDaddy.com, a następnie wybierz **Moje konto** , a następnie **Zarządzanie domenami Mój**.</span><span class="sxs-lookup"><span data-stu-id="06e28-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="06e28-111">Wybierz z menu rozwijanego dla nazwy domeny, które chcą korzystać z aplikacji sieci web platformy Azure i wybierz **zarządzania DNS**.</span><span class="sxs-lookup"><span data-stu-id="06e28-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![Domena niestandardowa strona GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="06e28-113">Z **szczegóły domeny** przewiń do **pliku strefy DNS** kartę.</span><span class="sxs-lookup"><span data-stu-id="06e28-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="06e28-114">Jest to sekcja używane do dodawania i modyfikowania rekordów DNS dla nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="06e28-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Karta pliku strefy DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="06e28-116">Wybierz **Dodaj rekord** można dodać istniejącego rekordu.</span><span class="sxs-lookup"><span data-stu-id="06e28-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="06e28-117">Aby **Edytuj** istniejącego rekordu, wybierz pióro & Papier ikona obok rekordu.</span><span class="sxs-lookup"><span data-stu-id="06e28-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06e28-118">Przed dodaniem nowych rekordów, należy zwrócić uwagę GoDaddy utworzył już rekordy DNS dla popularnych poddomen (o nazwie **hosta** w edytorze) takie jak **e-mail**, **pliki**, **poczty**i inne.</span><span class="sxs-lookup"><span data-stu-id="06e28-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="06e28-119">Jeśli nazwa, którą chcesz utworzyć, już istnieje, zmodyfikuj istniejący rekord zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="06e28-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="06e28-120">Podczas dodawania rekordu, musisz wybrać typ rekordu.</span><span class="sxs-lookup"><span data-stu-id="06e28-120">When adding a record, you must first select the record type.</span></span>
   
    ![Wybierz typ rekordu](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="06e28-122">Następnie należy podać **hosta** (domenę niestandardową lub domenę podrzędną) i jakie **wskazuje**.</span><span class="sxs-lookup"><span data-stu-id="06e28-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![Dodaj rekord strefy](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="06e28-124">Podczas dodawania **rekordu (hosta)** — należy ustawić **hosta** pole jednej  **@**  (Ta pozycja reprezentuje nazwę domeny głównej, takich jak **contoso.com** ,) * (symbol wieloznaczny dopasowania wielu domen podrzędnych,) lub domenę podrzędną, o których chcesz użyć (na przykład **www**.) Należy ustawić **wskazuje** pole na adres IP, aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06e28-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="06e28-125">Podczas dodawania **rekord CNAME (alias)** — należy ustawić **hosta** do domeny podrzędnej chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="06e28-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="06e28-126">Na przykład **www**.</span><span class="sxs-lookup"><span data-stu-id="06e28-126">For example, **www**.</span></span> <span data-ttu-id="06e28-127">Należy ustawić **wskazuje** do **. azurewebsites.net** nazwy domeny aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06e28-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="06e28-128">Na przykład **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="06e28-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="06e28-129">Kliknij przycisk **dodać kolejne**.</span><span class="sxs-lookup"><span data-stu-id="06e28-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="06e28-130">Wybierz **TXT** jako typ rekordu, następnie określ **hosta** wartość  **@**  i **wskazuje** wartość  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="06e28-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06e28-131">Ten rekord TXT jest używany przez usługę Azure można sprawdzić poprawności własnej domeny opisanego przez rekord A lub pierwszy rekord TXT.</span><span class="sxs-lookup"><span data-stu-id="06e28-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="06e28-132">Po zamapowaniu domeny aplikacji sieci web w portalu Azure można usunąć tego wpisu rekordu TXT.</span><span class="sxs-lookup"><span data-stu-id="06e28-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="06e28-133">Po zakończeniu dodawania lub modyfikowania rekordów, kliknij przycisk **Zakończ** można zapisać zmian.</span><span class="sxs-lookup"><span data-stu-id="06e28-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="06e28-134">Włącz nazwy domeny w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="06e28-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="06e28-135">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="06e28-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="06e28-136">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="06e28-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="06e28-137">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="06e28-137">What's changed</span></span>
* <span data-ttu-id="06e28-138">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="06e28-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

