---
title: "wydajność aaaConfigure ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure tooroute Traffic Manager ruchu toohello punktu końcowego o najniższym opóźnieniu"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="34db0-103">Konfigurowanie metody routingu ruchu hello wydajności</span><span class="sxs-lookup"><span data-stu-id="34db0-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="34db0-104">Witaj metody routingu ruchu wydajności umożliwia punktu końcowego toohello ruchu toodirect z hello można uzyskać najmniejsze opóźnienia sieci powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="34db0-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="34db0-105">Zazwyczaj datacenter hello o najniższym opóźnieniu hello jest hello najbliższej w odległości geograficznych.</span><span class="sxs-lookup"><span data-stu-id="34db0-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="34db0-106">Tej metody routingu ruchu nie można uwzględnić w czasie rzeczywistym zmiany w konfiguracji sieci lub obciążenia.</span><span class="sxs-lookup"><span data-stu-id="34db0-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="34db0-107">Metoda routingu tooconfigure wydajności</span><span class="sxs-lookup"><span data-stu-id="34db0-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="34db0-108">W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34db0-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="34db0-109">Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="34db0-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="34db0-110">Na pasku wyszukiwania portalu hello, wyszukaj hello **profilów usługi Traffic Manager** a następnie kliknij nazwę profilu hello, które tooconfigure hello metody routingu dla.</span><span class="sxs-lookup"><span data-stu-id="34db0-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="34db0-111">W hello **profilu usługi Traffic Manager** bloku, sprawdź, czy oba hello usługi w chmurze i witryn sieci Web mają tooinclude w konfiguracji są obecne.</span><span class="sxs-lookup"><span data-stu-id="34db0-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="34db0-112">W hello **ustawienia** kliknij **konfiguracji**w hello **konfiguracji** bloku ukończenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34db0-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="34db0-113">Dla **ustawienia metody routingu ruchu**, dla **metody routingu** wybierz **wydajności**.</span><span class="sxs-lookup"><span data-stu-id="34db0-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="34db0-114">Zestaw hello **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34db0-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="34db0-115">Wybierz odpowiednie hello **protokołu**i określ hello **portu** numer.</span><span class="sxs-lookup"><span data-stu-id="34db0-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="34db0-116">Aby uzyskać **ścieżki** wpisz ukośnik  */* .</span><span class="sxs-lookup"><span data-stu-id="34db0-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="34db0-117">punkty końcowe toomonitor, należy określić ścieżkę i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="34db0-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="34db0-118">A ukośnika "/" jest prawidłowym wpisem hello ścieżki względnej i wskazuje, czy plik hello znajduje się w katalogu głównym hello (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="34db0-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="34db0-119">U góry hello hello strony, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="34db0-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="34db0-120">Przetestuj hello zmiany w konfiguracji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34db0-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="34db0-121">Na pasku wyszukiwania portalu hello Wyszukaj nazwę profilu usługi Traffic Manager hello, a następnie kliknij przycisk hello profilu usługi Traffic Manager w wynikach hello tego hello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="34db0-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="34db0-122">W hello **Traffic Manager** bloku, kliknij opcję **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="34db0-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="34db0-123">Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="34db0-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="34db0-124">Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello.</span><span class="sxs-lookup"><span data-stu-id="34db0-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="34db0-125">W takim przypadku wszystkie żądania są punkt końcowy routingiem toohello o najniższym opóźnieniu hello z sieci powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="34db0-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="34db0-126">Po działa profilu Menedżera ruchu, należy edytować rekord DNS hello z autorytatywnych toopoint serwera DNS nazwę domeny firmowej domeny nazwa toohello Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="34db0-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Konfigurowanie metody routingu ruchu wydajności przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a><span data-ttu-id="34db0-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34db0-128">Next steps</span></span>

- <span data-ttu-id="34db0-129">Dowiedz się więcej o [ważone metody routingu ruchu](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="34db0-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="34db0-130">Dowiedz się więcej o [metody routingu priorytet](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="34db0-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="34db0-131">Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="34db0-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="34db0-132">Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="34db0-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png