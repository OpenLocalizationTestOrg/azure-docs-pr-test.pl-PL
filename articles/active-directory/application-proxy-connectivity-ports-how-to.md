---
title: aaaHow tooopen hello porty zapory wymagane dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Poprawnie dowiedzieć się, jakie porty tooopen dla toowork serwera Proxy aplikacji hello Azure AD"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="d9847-103">Jak tooopen hello porty zapory wymagane dla aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9847-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="d9847-104">toosee pełną listę hello wymagane porty i funkcję hello każdy port, zobacz sekcję wymagania wstępne hello hello [dokumentacji serwera Proxy aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="d9847-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="d9847-105">należy pamiętać, że serwer Proxy aplikacji tylko używa portów wychodzących.</span><span class="sxs-lookup"><span data-stu-id="d9847-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="d9847-106">Możesz również sprawdzić, czy masz wszystkie otwarte porty wymagane hello przez otwarcie hello [narzędzia Test porty łącznik](https://aadap-portcheck.connectorporttest.msappproxy.net/) z sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d9847-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="d9847-107">Więcej zaznaczeń zielony oznacza większą elastyczność.</span><span class="sxs-lookup"><span data-stu-id="d9847-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="d9847-108">Regiony serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9847-108">App Proxy regions</span></span>

<span data-ttu-id="d9847-109">Pracujemy nad sposób toolet wiesz, jakiego tych regionów musi toobe zielony dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d9847-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="d9847-110">Teraz upewnij się, że są one wszystkich.</span><span class="sxs-lookup"><span data-stu-id="d9847-110">For now, make sure they all are.</span></span> <span data-ttu-id="d9847-111">Środkowe stany USA jest również wymagany niezależnie od tego, w którym znajdują się w regionie.</span><span class="sxs-lookup"><span data-stu-id="d9847-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="d9847-112">toomake się hello narzędzie umożliwia hello prawo wyników, należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="d9847-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="d9847-113">Otwórz narzędzie hello w przeglądarce, z którym jest zainstalowany hello łącznika serwera hello.</span><span class="sxs-lookup"><span data-stu-id="d9847-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="d9847-114">Upewnij się, że wszystkie serwery proxy lub zapory tooyour dotyczy łącznika są również zastosować toothis strony.</span><span class="sxs-lookup"><span data-stu-id="d9847-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="d9847-115">Można to zrobić w programie Internet Explorer, przechodząc zbyt**ustawienia**  - &gt; **Opcje internetowe**  - &gt; **połączeń**  - &gt; **Ustawienia sieci Lan**.</span><span class="sxs-lookup"><span data-stu-id="d9847-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="d9847-116">Na tej stronie zobacz temat hello pola "Użyj serwera Proxy serwera dla your LAN".</span><span class="sxs-lookup"><span data-stu-id="d9847-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="d9847-117">Zaznacz to pole i umieść hello adres serwera proxy do pola "Address" hello.</span><span class="sxs-lookup"><span data-stu-id="d9847-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9847-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9847-118">Next steps</span></span>
[<span data-ttu-id="d9847-119">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9847-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
