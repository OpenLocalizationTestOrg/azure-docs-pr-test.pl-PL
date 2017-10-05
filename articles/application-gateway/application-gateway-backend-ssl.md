---
title: "Włączanie kompleksowej usługi SSL w usłudze Azure Application Gateway | Microsoft Docs"
description: "Ta strona zawiera omówienie kompleksowej obsługi protokołu SSL w usłudze Application Gateway."
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
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="5016c-103">Omówienie kompleksowej usługi SSL z usługą Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5016c-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="5016c-104">Usługa Application Gateway obsługuje przerywanie połączenia SSL na bramie, po którym ruch na ogół płynie niezaszyfrowany do serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5016c-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="5016c-105">Ta funkcja umożliwia odciążenie serwerów sieci Web z nadmiaru kosztownych operacji szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="5016c-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="5016c-106">Jednak dla niektórych klientów nieszyfrowana komunikacja z serwerami zaplecza jest opcją niemożliwą do zaakceptowania.</span><span class="sxs-lookup"><span data-stu-id="5016c-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="5016c-107">Nieszyfrowana komunikacja może być spowodowana przez wymagania dotyczące zabezpieczeń lub zgodności albo aplikacja może akceptować jedynie bezpieczne połączenia.</span><span class="sxs-lookup"><span data-stu-id="5016c-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="5016c-108">Na potrzeby takich aplikacji brama aplikacji obsługuje kompleksowe szyfrowanie SSL.</span><span class="sxs-lookup"><span data-stu-id="5016c-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="5016c-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5016c-109">Overview</span></span>

<span data-ttu-id="5016c-110">Kompleksowa usługa SSL pozwala na bezpieczne przesyłanie zaszyfrowanych danych poufnych do zaplecza, umożliwiając jednocześnie korzystanie z funkcji równoważenia obciążenia warstwy 7, które oferuje usługa Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="5016c-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="5016c-111">Do tych funkcji należą koligacja sesji oparta na plikach cookie, routing oparty na adresach URL, obsługa routingu opartego na witrynach lub możliwość iniekcji nagłówków X-Forwarded-*.</span><span class="sxs-lookup"><span data-stu-id="5016c-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="5016c-112">Po skonfigurowaniu kompleksowego trybu komunikacji SSL usługa Application Gateway kończy sesje SSL na bramie i odszyfrowuje ruch użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5016c-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="5016c-113">Następnie stosuje skonfigurowane reguły, aby wybrać odpowiednie wystąpienie puli serwerów zaplecza w celu skierowania do nich ruchu.</span><span class="sxs-lookup"><span data-stu-id="5016c-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="5016c-114">Następnie usługa Application Gateway inicjuje nowe połączenie SSL z serwerem zaplecza i ponownie szyfruje dane przy użyciu certyfikatu klucza publicznego serwera zaplecza przed przekazaniem żądania do zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5016c-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="5016c-115">Kompleksową usługę SSL można włączyć, konfigurując dla ustawienia protokołu BackendHTTPSetting wartość HTTPS, co jest następnie stosowane do puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5016c-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="5016c-116">Każdy serwer zaplecza w puli zaplecza z włączoną kompleksową usługą SSL należy skonfigurować przy użyciu certyfikatu, aby umożliwić bezpieczną komunikację.</span><span class="sxs-lookup"><span data-stu-id="5016c-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![Scenariusz kompleksowej usługi SSL][1]

<span data-ttu-id="5016c-118">W tym przykładzie żądania używające protokołu TLS 1.2 są kierowane do serwerów zaplecza w puli Pula1 za pomocą kompleksowej usługi SSL.</span><span class="sxs-lookup"><span data-stu-id="5016c-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="5016c-119">Kompleksowa usługa SSL i lista dozwolonych certyfikatów</span><span class="sxs-lookup"><span data-stu-id="5016c-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="5016c-120">Usługa Application Gateway komunikuje się tylko ze znanymi wystąpieniami zaplecza, których certyfikaty znajdują się na liście dozwolonych certyfikatów tej usługi.</span><span class="sxs-lookup"><span data-stu-id="5016c-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="5016c-121">Aby włączyć listę dozwolonych certyfikatów, należy przekazać klucz publiczny certyfikatów serwera zaplecza do usługi Application Gateway (nie certyfikat główny).</span><span class="sxs-lookup"><span data-stu-id="5016c-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="5016c-122">W takim przypadku możliwe będą tylko połączenia do znanych zapleczy, które znajdują się na liście dozwolonych.</span><span class="sxs-lookup"><span data-stu-id="5016c-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="5016c-123">Połączenia do pozostałych zapleczy zakończą się błędem bramy.</span><span class="sxs-lookup"><span data-stu-id="5016c-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="5016c-124">Certyfikaty z podpisem własnym są przeznaczone tylko do celów testowych i nie są zalecane dla obciążeń w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="5016c-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="5016c-125">Takie certyfikaty także muszą zostać umieszczone na liście dozwolonych usługi Application Gateway, jak opisano w poprzednich krokach, zanim będzie można ich użyć.</span><span class="sxs-lookup"><span data-stu-id="5016c-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5016c-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5016c-126">Next steps</span></span>

<span data-ttu-id="5016c-127">Po zapoznaniu się z kompleksową usługą SSL zapoznaj się z informacjami dotyczącymi [włączania kompleksowej usługi SSL w bramie aplikacji](application-gateway-end-to-end-ssl-powershell.md), aby utworzyć bramę aplikacji korzystającą z kompleksowej usługi SSL.</span><span class="sxs-lookup"><span data-stu-id="5016c-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
