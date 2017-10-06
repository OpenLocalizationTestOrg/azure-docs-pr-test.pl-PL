---
title: "aaaConfigure niestandardowej nazwy domeny w usłudze Azure App Service (GoDaddy)"
description: "Dowiedz się, jak nazwa toouse domeny z GoDaddy z aplikacjami sieci Web Azure"
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="29e49-103">Konfigurowanie nazwy domeny niestandardowej (kupionej bezpośrednio od firmy GoDaddy) w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="29e49-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="29e49-104">Jeśli została kupione domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure można znaleźć toohello ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="29e49-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="29e49-105">Ten artykuł zawiera instrukcje przy użyciu nazwy domeny niestandardowej, które zostało zakupione bezpośrednio z [GoDaddy](https://godaddy.com) z [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="29e49-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="29e49-106">Opis rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="29e49-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="29e49-107">Dodaj rekord DNS dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="29e49-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="29e49-108">tooassociate domeny niestandardowej z aplikacją sieci web w usłudze App Service, należy dodać nowy wpis w tabeli DNS powitania dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="29e49-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="29e49-109">Następujące kroki toolocate hello DNS hello użyj narzędzi dla GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="29e49-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="29e49-110">Logowanie na koncie tooyour z GoDaddy.com, a następnie wybierz **Moje konto** , a następnie **Zarządzanie domenami Mój**.</span><span class="sxs-lookup"><span data-stu-id="29e49-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="29e49-111">Menu rozwijanego wybierz hello hello nazwy domeny ma toouse z aplikacją sieci web platformy Azure, a następnie wybierz **zarządzania DNS**.</span><span class="sxs-lookup"><span data-stu-id="29e49-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![Domena niestandardowa strona GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="29e49-113">Z hello **szczegóły domeny** przewiń toohello **pliku strefy DNS** kartę. Jest to sekcja hello używane do dodawania i modyfikowania rekordów DNS dla nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="29e49-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Karta pliku strefy DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="29e49-115">Wybierz **Dodaj rekord** tooadd istniejącego rekordu.</span><span class="sxs-lookup"><span data-stu-id="29e49-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="29e49-116">zbyt**Edytuj** istniejącego rekordu, wybierz hello pióro & papieru ikona obok hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="29e49-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29e49-117">Przed dodaniem nowych rekordów, należy zwrócić uwagę GoDaddy utworzył już rekordy DNS dla popularnych poddomen (o nazwie **hosta** w edytorze) takie jak **e-mail**, **pliki**, **poczty**i inne.</span><span class="sxs-lookup"><span data-stu-id="29e49-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="29e49-118">Jeśli nazwa hello toouse ma już istnieje, zmodyfikuj istniejący rekord hello zamiast tworzenia nowej.</span><span class="sxs-lookup"><span data-stu-id="29e49-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="29e49-119">Podczas dodawania rekordu, musisz wybrać typ rekordu hello.</span><span class="sxs-lookup"><span data-stu-id="29e49-119">When adding a record, you must first select hello record type.</span></span>
   
    ![Wybierz typ rekordu](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="29e49-121">Następnie należy podać hello **hosta** (hello podrzędnej lub domeny niestandardowe) i jakie **wskazuje**.</span><span class="sxs-lookup"><span data-stu-id="29e49-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![Dodaj rekord strefy](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="29e49-123">Podczas dodawania **rekordu (hosta)** — należy ustawić hello **hosta** tooeither pola  **@**  (Ta pozycja reprezentuje nazwę domeny głównej, takich jak  **contoso.com**,) * (symbol wieloznaczny dopasowania wielu domen podrzędnych,) lub domenę podrzędną hello mają toouse (na przykład **www**.) Należy ustawić hello **wskazuje** pola adresu IP toohello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29e49-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="29e49-124">Podczas dodawania **rekord CNAME (alias)** — należy ustawić hello **hosta** domeny podrzędnej toohello pola mają toouse.</span><span class="sxs-lookup"><span data-stu-id="29e49-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="29e49-125">Na przykład **www**.</span><span class="sxs-lookup"><span data-stu-id="29e49-125">For example, **www**.</span></span> <span data-ttu-id="29e49-126">Należy ustawić hello **wskazuje** toohello pola **. azurewebsites.net** nazwy domeny aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29e49-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="29e49-127">Na przykład **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="29e49-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="29e49-128">Kliknij przycisk **dodać kolejne**.</span><span class="sxs-lookup"><span data-stu-id="29e49-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="29e49-129">Wybierz **TXT** jako typ rekordu hello, następnie określ **hosta** wartość  **@**  i **wskazuje** wartość  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="29e49-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29e49-130">Ten rekord TXT jest używany przez Azure toovalidate własnej się, że domena hello opisanego przez hello rekordu lub hello pierwszy rekord TXT.</span><span class="sxs-lookup"><span data-stu-id="29e49-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="29e49-131">Po hello domeny aplikacji sieci web toohello mapowane w hello portalu Azure, można usunąć tego wpisu rekordu TXT.</span><span class="sxs-lookup"><span data-stu-id="29e49-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="29e49-132">Po zakończeniu dodawania lub modyfikowania rekordów, kliknij przycisk **Zakończ** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="29e49-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="29e49-133">Włącz nazwy domeny hello na aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="29e49-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="29e49-134">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="29e49-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="29e49-135">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="29e49-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="29e49-136">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="29e49-136">What's changed</span></span>
* <span data-ttu-id="29e49-137">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="29e49-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

