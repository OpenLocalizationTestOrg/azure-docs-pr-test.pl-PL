---
title: "aaaEnabling zakończenia tooend protokół SSL dla bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie tooend zakończenia bramy aplikacji hello obsługi protokołu SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="daa3f-103">Przegląd końcowy tooend SSL z bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="daa3f-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="daa3f-104">Brama aplikacji w obsługuje kończenia żądań SSL na powitania bramy, po zwykle przepływu ruchu, który niezaszyfrowanej toohello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daa3f-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="daa3f-105">Ta funkcja umożliwia unburdened z kosztownych koszty szyfrowania i odszyfrowywania toobe serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="daa3f-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="daa3f-106">Jednak w przypadku niektórych klientów serwerów wewnętrznej bazy danych toohello niezaszyfrowane komunikacja nie jest dopuszczalne opcją.</span><span class="sxs-lookup"><span data-stu-id="daa3f-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="daa3f-107">Niezaszyfrowane komunikacji może być ze względu na wymagania toosecurity, wymagania dotyczące zgodności, lub aplikacja hello mogą tylko zaakceptować bezpiecznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="daa3f-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="daa3f-108">Dla takich aplikacji bramy aplikacji obsługuje zakończenia tooend protokołu SSL szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="daa3f-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="daa3f-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="daa3f-109">Overview</span></span>

<span data-ttu-id="daa3f-110">Tooend końcowych SSL pozwala toosecurely przesyłać szyfrowane, gdy nadal korzystanie z zalet funkcji równoważenia obciążenia warstwy 7 hello bramę aplikacji zawiera poufne dane toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daa3f-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="daa3f-111">Niektóre z tych funkcji są koligacji na podstawie plików cookie sesji, na podstawie adresu URL routingu, pomocy technicznej dla routingu na podstawie witryn lub możliwości tooinject X - przekazywane-* nagłówków.</span><span class="sxs-lookup"><span data-stu-id="daa3f-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="daa3f-112">Przy zastosowaniu trybu komunikacji SSL tooend zakończenia, brama aplikacji w kończy hello sesji SSL na powitania bramy i odszyfrowuje ruchu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="daa3f-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="daa3f-113">Stosuje następnie hello skonfigurowane reguły tooselect odpowiednie zaplecza puli wystąpienia tooroute ruchu.</span><span class="sxs-lookup"><span data-stu-id="daa3f-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="daa3f-114">Brama aplikacji w następnie inicjuje nowy serwer wewnętrznej bazy danych toohello połączenia SSL i ponownie szyfruje dane przy użyciu certyfikatu klucza publicznego serwera wewnętrznej bazy danych hello przed przesłaniem hello żądania toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daa3f-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="daa3f-115">Tooend zakończenia, który jest włączony protokół SSL, ustawiając ustawienia protokołu w tooHTTPS BackendHTTPSetting, który jest następnie stosowany tooa puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daa3f-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="daa3f-116">Każdy serwer wewnętrznej bazy danych w puli zaplecza hello z tooend zakończenia, który włączony protokół SSL musi mieć certyfikat tooallow bezpiecznej komunikacji.</span><span class="sxs-lookup"><span data-stu-id="daa3f-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![Scenariusz ssl tooend zakończenia][1]

<span data-ttu-id="daa3f-118">W tym przykładzie żądań przy użyciu TLS1.2 są serwerami routingiem toobackend w Pool1 przy użyciu tooend końcowych SSL.</span><span class="sxs-lookup"><span data-stu-id="daa3f-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="daa3f-119">Zakończenie tooend SSL i certyfikatów niedozwolonych</span><span class="sxs-lookup"><span data-stu-id="daa3f-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="daa3f-120">Brama aplikacji w komunikuje się tylko z zaplecza znane są wystąpienia białej swój certyfikat z bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="daa3f-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="daa3f-121">niedozwolonych tooenable certyfikaty, należy przekazać klucza publicznego hello bramy aplikacji toohello certyfikaty serwera wewnętrznej bazy danych (nie hello certyfikatu głównego).</span><span class="sxs-lookup"><span data-stu-id="daa3f-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="daa3f-122">Następnie dozwolone są tylko połączenia tooknown i białej zapleczy.</span><span class="sxs-lookup"><span data-stu-id="daa3f-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="daa3f-123">Witaj pozostałych zapleczy powoduje błąd bramy.</span><span class="sxs-lookup"><span data-stu-id="daa3f-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="daa3f-124">Certyfikaty z podpisem własnym są przeznaczone tylko do celów testowych i nie są zalecane dla obciążeń w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="daa3f-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="daa3f-125">Takie certyfikaty mają białej toobe z bramy aplikacji hello zgodnie z opisem w poprzednich krokach przed ich użyciem hello.</span><span class="sxs-lookup"><span data-stu-id="daa3f-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa3f-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="daa3f-126">Next steps</span></span>

<span data-ttu-id="daa3f-127">Po zapoznawanie tooend końcowych SSL, przejdź zbyt[włączyć tooend końcowych SSL na bramie aplikacji](application-gateway-end-to-end-ssl-powershell.md) toocreate bramy aplikacji przy użyciu kończyć tooend protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="daa3f-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
