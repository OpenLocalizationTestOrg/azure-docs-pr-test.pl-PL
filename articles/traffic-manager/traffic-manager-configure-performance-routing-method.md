---
title: "Konfigurowanie metody routingu ruchu wydajności przy użyciu usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania usługi Traffic Manager można kierować ruchem do punktu końcowego o najniższym opóźnieniu"
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
ms.openlocfilehash: 014aa646459cd64fca7c697419324caa3edaeeea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-performance-traffic-routing-method"></a><span data-ttu-id="c3e5a-103">Konfigurowanie metody routingu ruchu wydajności</span><span class="sxs-lookup"><span data-stu-id="c3e5a-103">Configure the performance traffic routing method</span></span>

<span data-ttu-id="c3e5a-104">Metody routingu ruchu wydajności umożliwia kierować ruch do punktu końcowego o najniższym opóźnieniu sieci klienta.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span></span> <span data-ttu-id="c3e5a-105">Zazwyczaj centrum danych z najniższym opóźnieniu jest najbardziej w odległości geograficznych.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span></span> <span data-ttu-id="c3e5a-106">Tej metody routingu ruchu nie można uwzględnić w czasie rzeczywistym zmiany w konfiguracji sieci lub obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="to-configure-performance-routing-method"></a><span data-ttu-id="c3e5a-107">Aby skonfigurować metody routingu wydajności</span><span class="sxs-lookup"><span data-stu-id="c3e5a-107">To configure performance routing method</span></span>

1. <span data-ttu-id="c3e5a-108">Z poziomu przeglądarki zaloguj się do witryny [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c3e5a-109">Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="c3e5a-110">Na pasku wyszukiwania portalu, wyszukaj **profilów usługi Traffic Manager** , a następnie kliknij nazwę profilu, który chcesz skonfigurować metody routingu.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="c3e5a-111">W **profilu usługi Traffic Manager** bloku, sprawdź, czy są obecne usługi w chmurze i witryn sieci Web, które mają zostać uwzględnione w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="c3e5a-112">W **ustawienia** kliknij **konfiguracji**i w **konfiguracji** bloku ukończenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c3e5a-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="c3e5a-113">Dla **ustawienia metody routingu ruchu**, dla **metody routingu** wybierz **wydajności**.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="c3e5a-114">Ustaw **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c3e5a-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="c3e5a-115">Wybierz odpowiednie **protokołu**, a następnie określ **portu** numer.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-115">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="c3e5a-116">Aby uzyskać **ścieżki** wpisz ukośnik  */* .</span><span class="sxs-lookup"><span data-stu-id="c3e5a-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="c3e5a-117">Aby monitorować punktów końcowych, należy określić ścieżkę i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-117">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="c3e5a-118">A ukośnika "/" jest prawidłowym wpisem dla ścieżki względnej i oznacza, że plik znajduje się w katalogu głównym (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="c3e5a-119">W górnej części strony kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-119">At the top of the page, click **Save**.</span></span>
5.  <span data-ttu-id="c3e5a-120">Testowanie zmian w konfiguracji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c3e5a-120">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="c3e5a-121">Na pasku wyszukiwania portalu, wyszukaj nazwę profilu Menedżera ruchu, a następnie kliknij przycisk profilu usługi Traffic Manager w wynikach który wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="c3e5a-122">W **Traffic Manager** bloku, kliknij opcję **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-122">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="c3e5a-123">**Profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS nowo utworzony profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="c3e5a-124">Może to służyć przez wszystkich klientów (na przykład, przechodząc do niej przy użyciu przeglądarki sieci web) do pobrania kierowane do prawej punktu końcowego jako określana przez typ routingu.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="c3e5a-125">W takim przypadku wszystkie żądania są kierowane do punktu końcowego o najniższym opóźnieniu sieci klienta.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span></span>
6. <span data-ttu-id="c3e5a-126">Po działa profilu Menedżera ruchu, należy edytować rekord DNS na z autorytatywnego serwera DNS, aby wskazywała nazwę domeny firmowej na nazwę domeny usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c3e5a-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Konfigurowanie metody routingu ruchu wydajności przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a><span data-ttu-id="c3e5a-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3e5a-128">Next steps</span></span>

- <span data-ttu-id="c3e5a-129">Dowiedz się więcej o [ważone metody routingu ruchu](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="c3e5a-130">Dowiedz się więcej o [metody routingu priorytet](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="c3e5a-131">Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="c3e5a-132">Dowiedz się, jak [Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c3e5a-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png