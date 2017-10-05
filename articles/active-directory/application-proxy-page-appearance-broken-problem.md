---
title: "Strona aplikacji nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Wskazówki, gdy strona nie jest prawidłowo wyświetlane w aplikacji serwer Proxy aplikacji jest zintegrowany z usługą Azure AD"
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="2562a-103">Strona aplikacji nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="2562a-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="2562a-104">W tym artykule ułatwiają rozwiązywanie problemów z aplikacji serwera Proxy usługi Azure Active Directory aplikacji, przejdź do strony, ale coś na stronie nie poprawna.</span><span class="sxs-lookup"><span data-stu-id="2562a-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="2562a-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2562a-105">Overview</span></span>
<span data-ttu-id="2562a-106">Podczas publikowania aplikacji serwera Proxy aplikacji tylko strony w katalogu głównym są dostępne podczas uzyskiwania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2562a-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="2562a-107">Jeśli strona nie jest poprawne wyświetlanie, adres URL wewnętrzny główny używany dla aplikacji może brakować niektórych zasobów strony.</span><span class="sxs-lookup"><span data-stu-id="2562a-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="2562a-108">Aby rozwiązać, upewnij się, po opublikowaniu *wszystkie* zasobów na stronie jako część aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2562a-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="2562a-109">Możesz sprawdzić, jest to problem, otwierając tracker Twojej sieci (takie jak Fiddler lub F12 narzędzia w Internet Explorer/krawędzi), podczas ładowania strony i wyszukiwanie błędów 404.</span><span class="sxs-lookup"><span data-stu-id="2562a-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="2562a-110">Wskazująca stron, które aktualnie nie można odnaleźć i muszą zostać opublikowane.</span><span class="sxs-lookup"><span data-stu-id="2562a-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="2562a-111">Na przykład ten przypadek założono po opublikowaniu aplikacji kosztów przy użyciu wewnętrznego adresu URL z <http://myapps/expenses>, ale aplikacja korzysta z arkusza stylów <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="2562a-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="2562a-112">W takim przypadku arkusza stylów nie jest opublikowana w aplikacji, dlatego podczas ładowania aplikacji kosztów zgłosić błąd 404 podczas próby załadowania style.css.</span><span class="sxs-lookup"><span data-stu-id="2562a-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="2562a-113">W tym przykładzie będzie można rozwiązać problemu, przez opublikowaniem aplikacji z wewnętrzny adres URL <http://myapp/> zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="2562a-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="2562a-114">Problemy z publikowaniem jako jedną aplikację</span><span class="sxs-lookup"><span data-stu-id="2562a-114">Problems with publishing as one application</span></span>

<span data-ttu-id="2562a-115">Jeśli nie jest możliwe do publikowania wszystkich zasobów w tej samej aplikacji, należy opublikować wiele aplikacji i włączyć łącza między nimi.</span><span class="sxs-lookup"><span data-stu-id="2562a-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="2562a-116">Aby to zrobić, zaleca się używanie [domen niestandardowych](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2562a-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="2562a-117">Jednak to rozwiązanie wymaga własny certyfikat dla domeny i aplikacji użyj w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="2562a-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="2562a-118">Inne opcje, zobacz [Rozwiązywanie problemów z dokumentacji uszkodzonych łączy](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="2562a-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2562a-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2562a-119">Next steps</span></span>
[<span data-ttu-id="2562a-120">Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2562a-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
