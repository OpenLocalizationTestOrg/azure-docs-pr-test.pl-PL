---
title: "Konfigurowanie metody routingu ruchu okrężnego ważoną przy użyciu usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób równoważenia obciążenia ruchu przy użyciu metody okrężnego w usłudze Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="61f33-103">Konfigurowanie metody routingu ruchu ważoną w usłudze Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="61f33-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="61f33-104">Wzorzec typowe metody routingu ruchu jest udostępniają zestaw identyczne punkty końcowe, które obejmują usługi w chmurze i witryn sieci Web, i przesyłają dane do każdej z nich w działaniu okrężnym.</span><span class="sxs-lookup"><span data-stu-id="61f33-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="61f33-105">Poniższe kroki przedstawiają sposób konfigurowania tego typu metody routingu ruchu.</span><span class="sxs-lookup"><span data-stu-id="61f33-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="61f33-106">Witryn sieci Web Azure zapewniają już obciążenia okrężnego równoważenia funkcji dla witryn sieci Web w centrum danych (regionu).</span><span class="sxs-lookup"><span data-stu-id="61f33-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="61f33-107">Traffic Manager służy do określenia metody routingu ruchu okrężnego dla witryn sieci Web w różnych centrach danych.</span><span class="sxs-lookup"><span data-stu-id="61f33-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="61f33-108">Aby skonfigurować metody routingu ruchu ważoną</span><span class="sxs-lookup"><span data-stu-id="61f33-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="61f33-109">Z poziomu przeglądarki zaloguj się do witryny [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61f33-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="61f33-110">Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="61f33-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="61f33-111">Na pasku wyszukiwania portalu, wyszukaj **profilów usługi Traffic Manager** , a następnie kliknij nazwę profilu, który chcesz skonfigurować metody routingu.</span><span class="sxs-lookup"><span data-stu-id="61f33-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="61f33-112">W **profilu usługi Traffic Manager** bloku, sprawdź, czy są obecne usługi w chmurze i witryn sieci Web, które mają zostać uwzględnione w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61f33-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="61f33-113">W **ustawienia** kliknij **konfiguracji**i w **konfiguracji** bloku ukończenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="61f33-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="61f33-114">Aby uzyskać **ustawienia metody routingu ruchu**, sprawdź, czy metody routingu ruchu **ważone**.</span><span class="sxs-lookup"><span data-stu-id="61f33-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="61f33-115">Jeśli nie, kliknij przycisk **ważone** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="61f33-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="61f33-116">Ustaw **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="61f33-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="61f33-117">Wybierz odpowiednie **protokołu**, a następnie określ **portu** numer.</span><span class="sxs-lookup"><span data-stu-id="61f33-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="61f33-118">Aby uzyskać **ścieżki** wpisz ukośnik  */* .</span><span class="sxs-lookup"><span data-stu-id="61f33-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="61f33-119">Aby monitorować punktów końcowych, należy określić ścieżkę i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="61f33-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="61f33-120">A ukośnika "/" jest prawidłowym wpisem dla ścieżki względnej i oznacza, że plik znajduje się w katalogu głównym (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="61f33-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="61f33-121">W górnej części strony kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="61f33-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="61f33-122">Testowanie zmian w konfiguracji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="61f33-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="61f33-123">Na pasku wyszukiwania portalu, wyszukaj nazwę profilu Menedżera ruchu, a następnie kliknij przycisk profilu usługi Traffic Manager w wynikach który wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="61f33-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="61f33-124">W **Traffic Manager** bloku, kliknij opcję **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="61f33-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="61f33-125">**Profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS nowo utworzony profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="61f33-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="61f33-126">Może to służyć przez wszystkich klientów (na przykład, przechodząc do niej przy użyciu przeglądarki sieci web) do pobrania kierowane do prawej punktu końcowego jako określana przez typ routingu.</span><span class="sxs-lookup"><span data-stu-id="61f33-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="61f33-127">W takim przypadku wszystkie żądania są kierowane każdego punktu końcowego w działaniu okrężnym.</span><span class="sxs-lookup"><span data-stu-id="61f33-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="61f33-128">Po działa profilu Menedżera ruchu, należy edytować rekord DNS na z autorytatywnego serwera DNS, aby wskazywała nazwę domeny firmowej na nazwę domeny usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="61f33-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Konfigurowanie metody routingu ruchu ważoną przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a><span data-ttu-id="61f33-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61f33-130">Next steps</span></span>

- <span data-ttu-id="61f33-131">Dowiedz się więcej o [Metoda routingu ruchu priorytet](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="61f33-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="61f33-132">Dowiedz się więcej o [wydajności Metoda routingu ruchu](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="61f33-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="61f33-133">Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="61f33-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="61f33-134">Dowiedz się, jak [Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="61f33-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
