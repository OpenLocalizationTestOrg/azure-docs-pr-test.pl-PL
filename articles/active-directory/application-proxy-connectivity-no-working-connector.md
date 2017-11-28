---
title: "Znaleziono aaaNo pracy łącznika grupy dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Rozwiąż problemy, które mogą wystąpić po nie pracy łącznika w grupie łącznika dla aplikacji z powitania serwera Proxy aplikacji usługi Azure AD"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="88881-103">Nie znaleziono aplikacji serwera Proxy aplikacji grupy łącznika pracy</span><span class="sxs-lookup"><span data-stu-id="88881-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="88881-104">Ten artykuł pomocy możesz tooresolve hello typowych problemów, które muszą ponieść gdy nie jest łącznika dla aplikacji serwera Proxy aplikacji wykryte zintegrowane z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="88881-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="88881-105">Omówienie kroków</span><span class="sxs-lookup"><span data-stu-id="88881-105">Overview of steps</span></span>
<span data-ttu-id="88881-106">Jeśli nie ma żadnych pracy łącznika w grupie łącznika dla aplikacji, istnieje kilka sposobów tooresolve hello problemu:</span><span class="sxs-lookup"><span data-stu-id="88881-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="88881-107">Jeśli w grupie hello nie łączników, można:</span><span class="sxs-lookup"><span data-stu-id="88881-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="88881-108">Pobierz nowy łącznik na powitania serwera lokalnego prawo i przypisz go toothis grupy</span><span class="sxs-lookup"><span data-stu-id="88881-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="88881-109">Przenieś do grupy hello łącznika usługi active</span><span class="sxs-lookup"><span data-stu-id="88881-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="88881-110">Jeśli nie łączniki active w grupie hello, można:</span><span class="sxs-lookup"><span data-stu-id="88881-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="88881-111">Zidentyfikowanie przyczyny hello Twojego łącznika jest nieaktywny i rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="88881-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="88881-112">Przenieś do grupy hello łącznika usługi active</span><span class="sxs-lookup"><span data-stu-id="88881-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="88881-113">tooknow, który z nich jest hello problem, otwórz menu "Serwer Proxy aplikacji" hello w aplikacji i przyjrzyj komunikat ostrzegawczy hello grupy łącznika.</span><span class="sxs-lookup"><span data-stu-id="88881-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="88881-114">Określ ją tej grupy hello wymaga co najmniej jeden łącznik (użytkownik nie masz żadnej grupy hello) lub że nie ma żadnych aktywnych łączników (Jeśli masz prawdopodobnie nieaktywne łączniki).</span><span class="sxs-lookup"><span data-stu-id="88881-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Wybór grupy łącznika w portalu Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="88881-116">Aby uzyskać szczegółowe informacje na każdej z tych opcji zobacz hello odpowiedniej sekcji poniżej.</span><span class="sxs-lookup"><span data-stu-id="88881-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="88881-117">Każdy z tych przyjęto założenie, uruchamiasz ze strony Zarządzanie hello łącznika.</span><span class="sxs-lookup"><span data-stu-id="88881-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="88881-118">Jeśli przeglądasz hello komunikat o błędzie powyżej, można przejść przez kliknięcie komunikatu ostrzegawczego hello toothis strony.</span><span class="sxs-lookup"><span data-stu-id="88881-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="88881-119">W przeciwnym razie ten znajduje się zbyt przechodząc**usługi Azure Active Directory**, klikając pozycję na **aplikacje dla przedsiębiorstw**, następnie **serwera Proxy aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="88881-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Łącznik grupy zarządzania w portalu Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="88881-121">Pobierz nowy łącznik</span><span class="sxs-lookup"><span data-stu-id="88881-121">Download a new Connector</span></span>

<span data-ttu-id="88881-122">toodownload nowy łącznik, użyj przycisku "Pobierz łącznik" hello u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="88881-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="88881-123">Uwaga hello łącznika potrzeb toobe zainstalowany na komputerze z aplikacją zaplecza toohello bezpośredniego procesów z wiersza i zwykle znajduje się na hello tym samym serwerze co aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="88881-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="88881-124">Po pobraniu hello łącznika powinna pojawić się w tym menu.</span><span class="sxs-lookup"><span data-stu-id="88881-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="88881-125">Kliknij hello łącznika, a następnie użyj toomake listy rozwijanej "Łącznik grupy" hello się, że należy toohello prawo grupy.</span><span class="sxs-lookup"><span data-stu-id="88881-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="88881-126">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="88881-126">Save hello change.</span></span>

   ![Pobierz łącznik hello z hello portalu Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="88881-128">Przenieś łącznika usługi Active</span><span class="sxs-lookup"><span data-stu-id="88881-128">Move an Active Connector</span></span>

<span data-ttu-id="88881-129">Jeśli masz łącznika usługi active muszą należeć do grupy toohello i ma aplikacji zaplecza docelowej toohello procesów z wiersza hello łącznika można przenieść do grupy hello przypisane.</span><span class="sxs-lookup"><span data-stu-id="88881-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="88881-130">toodo tak, kliknij przycisk hello łącznika.</span><span class="sxs-lookup"><span data-stu-id="88881-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="88881-131">W polu "Łącznik grupy" hello Użyj hello tooselect listy rozwijanej hello prawidłowej grupy, a następnie kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="88881-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="88881-132">Rozwiąż nieaktywne łącznika</span><span class="sxs-lookup"><span data-stu-id="88881-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="88881-133">Czy hello tylko łączników w grupie hello są nieaktywne, mogą mieć na komputerze, na którym nie ma odblokowany wszystkie porty niezbędne hello.</span><span class="sxs-lookup"><span data-stu-id="88881-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="88881-134">Zobacz porty hello dokumentu rozwiązywanie szczegółowe informacje dotyczące badania ten problem.</span><span class="sxs-lookup"><span data-stu-id="88881-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88881-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88881-135">Next steps</span></span>
[<span data-ttu-id="88881-136">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88881-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


