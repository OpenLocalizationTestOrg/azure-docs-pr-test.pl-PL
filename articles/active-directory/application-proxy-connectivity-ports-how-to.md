---
title: "Jak otworzyć porty zapory wymagane dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedzieć się, jakie porty do otwarcia dla aplikacji serwera Proxy Azure AD działała prawidłowo"
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="48c22-103">Jak otworzyć porty zapory wymagane dla aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="48c22-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="48c22-104">Aby wyświetlić pełną listę wymagane porty i funkcji każdy port, zobacz sekcję wymagania wstępne [dokumentacji serwera Proxy aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="48c22-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="48c22-105">należy pamiętać, że serwer Proxy aplikacji tylko używa portów wychodzących.</span><span class="sxs-lookup"><span data-stu-id="48c22-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="48c22-106">Możesz również sprawdzić, czy znajdują się wszystkie wymagane porty Otwórz otwierając [narzędzia Test porty łącznik](https://aadap-portcheck.connectorporttest.msappproxy.net/) z sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="48c22-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="48c22-107">Więcej zaznaczeń zielony oznacza większą elastyczność.</span><span class="sxs-lookup"><span data-stu-id="48c22-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="48c22-108">Regiony serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="48c22-108">App Proxy regions</span></span>

<span data-ttu-id="48c22-109">Pracujemy nad sposobem informacją o tym, które z tych regionów, musi być zielona dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="48c22-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="48c22-110">Teraz upewnij się, że są one wszystkich.</span><span class="sxs-lookup"><span data-stu-id="48c22-110">For now, make sure they all are.</span></span> <span data-ttu-id="48c22-111">Środkowe stany USA jest również wymagany niezależnie od tego, w którym znajdują się w regionie.</span><span class="sxs-lookup"><span data-stu-id="48c22-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="48c22-112">Aby upewnij się, że narzędzie daje prawo wyników, należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="48c22-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="48c22-113">Otwórz narzędzie w przeglądarce z serwera, na którym zainstalowano łącznik.</span><span class="sxs-lookup"><span data-stu-id="48c22-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="48c22-114">Upewnij się, że wszystkie serwery proxy lub zapory mające zastosowanie do Twojego łącznika również są stosowane do tej strony.</span><span class="sxs-lookup"><span data-stu-id="48c22-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="48c22-115">Można to zrobić w programie Internet Explorer, przechodząc do **ustawienia**  - &gt; **Opcje internetowe**  - &gt; **połączeń**  - &gt; **ustawienia sieci Lan**.</span><span class="sxs-lookup"><span data-stu-id="48c22-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="48c22-116">Na tej stronie zobacz temat pola "Użyj serwera Proxy serwera dla your LAN".</span><span class="sxs-lookup"><span data-stu-id="48c22-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="48c22-117">Zaznacz to pole i umieścić adres serwera proxy w polu "Address".</span><span class="sxs-lookup"><span data-stu-id="48c22-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c22-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48c22-118">Next steps</span></span>
[<span data-ttu-id="48c22-119">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c22-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
