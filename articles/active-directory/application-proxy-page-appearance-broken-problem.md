---
title: "Strona aaaApplication nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące po stronie powitania nie jest prawidłowo wyświetlane w aplikacji serwer Proxy aplikacji jest zintegrowany z usługą Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="e893d-103">Strona aplikacji nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="e893d-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="e893d-104">W tym artykule pomocy tootroubleshoot problemy z aplikacjami serwera Proxy usługi Azure Active Directory aplikacji po przejściu toohello strony, ale coś na stronie powitania wygląda prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="e893d-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="e893d-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e893d-105">Overview</span></span>
<span data-ttu-id="e893d-106">Podczas publikowania aplikacji serwera Proxy aplikacji tylko strony w katalogu głównym są dostępne podczas uzyskiwania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e893d-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="e893d-107">Jeśli na stronie powitania nie jest wyświetlane prawidłowo, hello głównego wewnętrzny adres URL użyty dla aplikacji hello może brakować niektórych zasobów strony.</span><span class="sxs-lookup"><span data-stu-id="e893d-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="e893d-108">tooresolve, upewnij się, że po opublikowaniu *wszystkie* hello zasobów na stronie powitania w ramach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e893d-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="e893d-109">Możesz sprawdzić to problemu hello otwierając tracker Twojej sieci (takie jak Fiddler lub F12 narzędzia w Internet Explorer/krawędzi), ładowanie strony hello i wyszukiwanie błędów 404.</span><span class="sxs-lookup"><span data-stu-id="e893d-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="e893d-110">Wskazująca hello strony, które aktualnie nie można odnaleźć i może być konieczne toobe opublikowane.</span><span class="sxs-lookup"><span data-stu-id="e893d-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="e893d-111">Na przykład ten przypadek założono po opublikowaniu aplikacji kosztów przy użyciu wewnętrznego adresu URL z <http://myapps/expenses>, ale aplikacja hello korzysta z arkusza stylów hello <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="e893d-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="e893d-112">W takim przypadku arkusza stylów hello nie jest opublikowana w aplikacji, więc ładowania aplikacji kosztów hello zgłosić błąd 404 podczas style.css tooload w trakcie.</span><span class="sxs-lookup"><span data-stu-id="e893d-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="e893d-113">W tym przykładzie będzie można rozwiązać problemu hello, publikując aplikacji hello z wewnętrzny adres URL <http://myapp/> zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="e893d-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="e893d-114">Problemy z publikowaniem jako jedną aplikację</span><span class="sxs-lookup"><span data-stu-id="e893d-114">Problems with publishing as one application</span></span>

<span data-ttu-id="e893d-115">Jeśli nie jest możliwe toopublish wszystkie zasoby w hello tej samej aplikacji, należy toopublish wiele aplikacji i włączyć łącza między nimi.</span><span class="sxs-lookup"><span data-stu-id="e893d-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="e893d-116">toodo tak, zaleca się używanie hello [domen niestandardowych](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e893d-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="e893d-117">Jednak to rozwiązanie wymaga własnej hello certyfikat dla domeny i aplikacji użyj w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="e893d-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="e893d-118">Inne opcje, zobacz hello [Rozwiązywanie problemów z dokumentacji uszkodzonych łączy](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="e893d-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e893d-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e893d-119">Next steps</span></span>
[<span data-ttu-id="e893d-120">Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e893d-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
