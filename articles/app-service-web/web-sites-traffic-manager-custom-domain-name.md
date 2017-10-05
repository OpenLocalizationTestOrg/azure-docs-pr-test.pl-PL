---
title: "Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service, który używa Menedżera ruchu do równoważenia obciążenia."
description: "Użyj nazwy domeny niestandardowej dla aplikacji sieci web w usłudze Azure App Service, która obejmuje usługi Traffic Manager w programie Równoważenie obciążenia."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="0b30d-103">Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service przy użyciu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="0b30d-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="0b30d-104">Ten artykuł zawiera ogólne instrukcje dotyczące korzystania z usługi Azure App Service przy użyciu niestandardowej nazwy domeny, korzystających z usługi Traffic Manager w celu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0b30d-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="0b30d-105">Opis rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="0b30d-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="0b30d-106">Konfigurowanie aplikacji sieci web dla Tryb standardowy</span><span class="sxs-lookup"><span data-stu-id="0b30d-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="0b30d-107">Dodaj rekord DNS dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="0b30d-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="0b30d-108">Jeśli zostały nabyte domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure Pomiń następujące kroki i odwoływać się do ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0b30d-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="0b30d-109">Aby skojarzyć domenę niestandardową z aplikacji sieci web w usłudze Azure App Service, niezbędny nowy wpis w tabeli DNS dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez rejestratora domen, zakupionym z nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="0b30d-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="0b30d-110">Wykonaj następujące kroki, aby zlokalizować i korzystania z narzędzi DNS.</span><span class="sxs-lookup"><span data-stu-id="0b30d-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="0b30d-111">Zaloguj się na koncie u rejestratora domen i poszukaj stronę Zarządzanie rekordami DNS.</span><span class="sxs-lookup"><span data-stu-id="0b30d-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="0b30d-112">Wyszukaj łącza lub obszarów witryny oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="0b30d-113">Często łącze do tej strony można znaleźć wyświetlanie informacji o koncie, a następnie sprawdzając takich jak łącze **mojej domeny**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="0b30d-114">Po znalezieniu strony zarządzania dla nazwy domeny, poszukaj łącza, który służy do edytowania rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="0b30d-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="0b30d-115">Może to być wymieniona jako **pliku strefy**, **rekordy DNS**, lub jako **zaawansowane** link konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0b30d-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="0b30d-116">Strona najprawdopodobniej będzie mieć kilka rekordów już utworzone, takich jak kojarzenie wpis "**@**"lub"\*" ze stroną "postojowego domeny".</span><span class="sxs-lookup"><span data-stu-id="0b30d-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="0b30d-117">Może również zawierać rekordy dotyczące typowych poddomen takich jak **www**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="0b30d-118">Strona będzie zawierać **rekordy CNAME**, lub Udostępnij listy rozwijanej wybierz typ rekordu.</span><span class="sxs-lookup"><span data-stu-id="0b30d-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="0b30d-119">Go może również zawierać inne rekordy takich jak **rekordy** i **rekordów MX**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="0b30d-120">W niektórych przypadkach rekordy CNAME zostanie wywołana przez inne nazwy, takie jak **rekord aliasu**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="0b30d-121">Strony będą także mieć pól, które umożliwiają **mapy** z **nazwy hosta** lub **nazwy domeny** na inną nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="0b30d-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="0b30d-122">Gdy specyfice każdy Rejestrator różnią się ogólnie mapowania *z* niestandardową nazwę domeny (takich jak **contoso.com**,) *do* nazwę domeny usługi Traffic Manager (**contoso.trafficmanager.net**) używany dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0b30d-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b30d-123">Alternatywnie Jeśli rekord jest już w użyciu, i chcesz preemptively powiązać go z aplikacji, można utworzyć dodatkowy rekord CNAME.</span><span class="sxs-lookup"><span data-stu-id="0b30d-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="0b30d-124">Na przykład, aby powiązać preemptively **www.contoso.com** do aplikacji sieci web, należy utworzyć rekord CNAME z **awverify.www** do **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="0b30d-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="0b30d-125">Następnie można dodać "www.contoso.com" do aplikacji sieci Web bez konieczności zmieniania rekord CNAME "www".</span><span class="sxs-lookup"><span data-stu-id="0b30d-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="0b30d-126">Aby uzyskać więcej informacji, zobacz [rekordy DNS Utwórz dla aplikacji sieci web w domenie niestandardowych][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="0b30d-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="0b30d-127">Po zakończeniu dodawania lub modyfikowania rekordów DNS u rejestratora, Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="0b30d-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="0b30d-128">Menedżer ruchu</span><span class="sxs-lookup"><span data-stu-id="0b30d-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="0b30d-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b30d-129">Next steps</span></span>
<span data-ttu-id="0b30d-130">Aby uzyskać więcej informacji, odwiedź stronę [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="0b30d-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
