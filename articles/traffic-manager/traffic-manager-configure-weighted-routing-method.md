---
title: "aaaConfigure ważone działanie okrężne ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooload równoważenie ruchu przy użyciu metody okrężnego w usłudze Traffic Manager"
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="00d92-103">Konfigurowanie metody routingu ruchu hello ważone w usłudze Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="00d92-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="00d92-104">Wzorzec typowe metody routingu ruchu jest tooprovide zbiór identyczne punkty końcowe, które obejmują usługi w chmurze i witryn sieci Web i wysyłania ruchu tooeach w działaniu okrężnym.</span><span class="sxs-lookup"><span data-stu-id="00d92-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="00d92-105">Witaj następujące kroki przedstawiają sposób tooconfigure to typ Metoda routingu ruchu.</span><span class="sxs-lookup"><span data-stu-id="00d92-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="00d92-106">Witryn sieci Web Azure zapewniają już obciążenia okrężnego równoważenia funkcji dla witryn sieci Web w centrum danych (regionu).</span><span class="sxs-lookup"><span data-stu-id="00d92-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="00d92-107">Menedżer ruchu umożliwia toospecify metody routingu ruchu okrężnego dla witryn sieci Web w różnych centrach danych.</span><span class="sxs-lookup"><span data-stu-id="00d92-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="00d92-108">metody routingu ruchu hello ważone tooconfigure</span><span class="sxs-lookup"><span data-stu-id="00d92-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="00d92-109">W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00d92-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="00d92-110">Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="00d92-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="00d92-111">Na pasku wyszukiwania portalu hello, wyszukaj hello **profilów usługi Traffic Manager** a następnie kliknij nazwę profilu hello, które tooconfigure hello metody routingu dla.</span><span class="sxs-lookup"><span data-stu-id="00d92-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="00d92-112">W hello **profilu usługi Traffic Manager** bloku, sprawdź, czy oba hello usługi w chmurze i witryn sieci Web mają tooinclude w konfiguracji są obecne.</span><span class="sxs-lookup"><span data-stu-id="00d92-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="00d92-113">W hello **ustawienia** kliknij **konfiguracji**w hello **konfiguracji** bloku ukończenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="00d92-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="00d92-114">Aby uzyskać **ustawienia metody routingu ruchu**, sprawdź, czy metody routingu ruchu hello **ważone**.</span><span class="sxs-lookup"><span data-stu-id="00d92-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="00d92-115">Jeśli nie, kliknij przycisk **ważone** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="00d92-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="00d92-116">Zestaw hello **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="00d92-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="00d92-117">Wybierz odpowiednie hello **protokołu**i określ hello **portu** numer.</span><span class="sxs-lookup"><span data-stu-id="00d92-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="00d92-118">Aby uzyskać **ścieżki** wpisz ukośnik  */* .</span><span class="sxs-lookup"><span data-stu-id="00d92-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="00d92-119">punkty końcowe toomonitor, należy określić ścieżkę i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="00d92-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="00d92-120">A ukośnika "/" jest prawidłowym wpisem hello ścieżki względnej i wskazuje, czy plik hello znajduje się w katalogu głównym hello (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="00d92-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="00d92-121">U góry hello hello strony, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="00d92-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="00d92-122">Przetestuj hello zmiany w konfiguracji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="00d92-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="00d92-123">Na pasku wyszukiwania portalu hello Wyszukaj nazwę profilu usługi Traffic Manager hello, a następnie kliknij przycisk hello profilu usługi Traffic Manager w wynikach hello tego hello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="00d92-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="00d92-124">W hello **Traffic Manager** bloku, kliknij opcję **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="00d92-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="00d92-125">Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="00d92-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="00d92-126">Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello.</span><span class="sxs-lookup"><span data-stu-id="00d92-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="00d92-127">W takim przypadku wszystkie żądania są kierowane każdego punktu końcowego w działaniu okrężnym.</span><span class="sxs-lookup"><span data-stu-id="00d92-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="00d92-128">Po działa profilu Menedżera ruchu, należy edytować rekord DNS hello z autorytatywnych toopoint serwera DNS nazwę domeny firmowej domeny nazwa toohello Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="00d92-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Konfigurowanie metody routingu ruchu ważoną przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a><span data-ttu-id="00d92-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="00d92-130">Next steps</span></span>

- <span data-ttu-id="00d92-131">Dowiedz się więcej o [Metoda routingu ruchu priorytet](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="00d92-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="00d92-132">Dowiedz się więcej o [wydajności Metoda routingu ruchu](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="00d92-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="00d92-133">Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="00d92-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="00d92-134">Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="00d92-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
