---
title: "Tworzenie aplikacji usługi Azure Mobile Engagement | Microsoft Docs"
description: "Artykuł opisuje sposób tworzenia nowej kolekcji aplikacji usługi Mobile Engagement na platformie Azure i rozpoczynania zarządzania aplikacjami za pomocą portalu Mobile Engagement."
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b8aa1798-28c6-424c-a5b5-8a264d5a0ff0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 47c1e122f6f38654cd63bb59e50e68803f76c83d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-mobile-engagement-app"></a><span data-ttu-id="f2626-103">Tworzenie aplikacji usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f2626-103">Create an Azure Mobile Engagement App</span></span>
<span data-ttu-id="f2626-104">W tym artykule opisano sposób wykorzystania metody **Szybkie tworzenie** do utworzenia aplikacji usługi **Azure Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="f2626-104">This article shows how to use the **Quick Create** method to create a new **Azure Mobile Engagement** App.</span></span> <span data-ttu-id="f2626-105">Artykuł opisuje również sposób przejścia do portalu **Mobile Engagement** w celu rozpoczęcia monitorowania aplikacji i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="f2626-105">The article also shows how to navigate to your **Mobile Engagement** portal in order to start monitoring and managing your apps.</span></span> 

<span data-ttu-id="f2626-106">Pamiętaj, że musisz dodać minimalny zestaw „podstawowej integracji”, aby korzystać z funkcji zbierania danych dla aplikacji i wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="f2626-106">Note that you must add a minimum set of "basic integration" in order to be able to collect data for your app and send push notifications.</span></span> <span data-ttu-id="f2626-107">Kompletna dokumentacja integracji znajduje się w sekcji [Mobile Engagement integration](mobile-engagement-windows-store-integrate-engagement.md) (Integracja usługi Mobile Engagement).</span><span class="sxs-lookup"><span data-stu-id="f2626-107">The complete integration documentation can be found in the [Mobile Engagement integration](mobile-engagement-windows-store-integrate-engagement.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2626-108">Aby ukończyć jakikolwiek samouczek usługi Azure Mobile Engagement, musisz mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f2626-108">To complete any Azure Mobile Engagement tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f2626-109">Jeśli nie masz konta, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f2626-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f2626-110">Aby uzyskać szczegółowe informacje, zobacz <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="f2626-110">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-mobile-app-in-azure"></a><span data-ttu-id="f2626-111">Konfigurowanie usługi Mobile Engagement dla aplikacji mobilnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f2626-111">Setup Mobile Engagement for your mobile app in Azure</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="navigate-to-your-mobile-engagement-portal"></a><span data-ttu-id="f2626-112">Przechodzenie do portalu Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f2626-112">Navigate to your Mobile Engagement portal</span></span>
<span data-ttu-id="f2626-113">Aby rozpocząć monitorowanie aplikacji i zarządzanie nią, przejdź do portalu Mobile Engagement, klikając przycisk **Portal Engagement** na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="f2626-113">To start monitoring and managing your application, navigate to your Mobile Engagement portal by clicking the **Engagement portal** button in the top bar.</span></span>

<span data-ttu-id="f2626-114">Po przejściu do portalu Mobile Engagement możesz analizować i tworzyć segmenty, zarządzać nimi, komunikować się z użytkownikami itp. Dostępne funkcje to m.in.:</span><span class="sxs-lookup"><span data-stu-id="f2626-114">Once you are in the  Mobile Engagement portal, you can analyze, create and manage segments, reach out to the users, etc.:</span></span>    

* [<span data-ttu-id="f2626-115">Monitorowanie danych aplikacji w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f2626-115">Monitor real time data about your application</span></span>](mobile-engagement-user-interface-monitor.md)
* [<span data-ttu-id="f2626-116">Analizowanie danych historycznych dotyczących aplikacji</span><span class="sxs-lookup"><span data-stu-id="f2626-116">Analyze historical data about your application</span></span>](mobile-engagement-user-interface-analytics.md)
* [<span data-ttu-id="f2626-117">Tworzenie i zarządzanie segmentami użytkowników w celu identyfikowania wzorców użycia</span><span class="sxs-lookup"><span data-stu-id="f2626-117">Create and manage segments of users to identify usage patterns</span></span>](mobile-engagement-user-interface-segments.md)
* [<span data-ttu-id="f2626-118">Docieranie do użytkowników aplikacji za pomocą powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="f2626-118">Reach out to the users of your application with push notifications</span></span>](mobile-engagement-user-interface-reach.md)

## <a name="see-also"></a><span data-ttu-id="f2626-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f2626-119">See Also</span></span>
[<span data-ttu-id="f2626-120">Definiowanie strategii Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f2626-120">Define your Mobile Engagement strategy</span></span>](mobile-engagement-define-your-mobile-engagement-strategy.md)

<span data-ttu-id="f2626-121">[Get started with Azure Mobile Engagement](mobile-engagement-windows-store-dotnet-get-started.md) (Rozpoczynanie pracy z usługą Azure Mobile Engagemenet) (możesz wybrać inne platformy mobilne w górnej części strony).</span><span class="sxs-lookup"><span data-stu-id="f2626-121">[Get started with Azure Mobile Engagement](mobile-engagement-windows-store-dotnet-get-started.md) (you can select other mobile platforms at the top of the page).</span></span>

