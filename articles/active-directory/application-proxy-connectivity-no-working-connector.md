---
title: "Znaleziono żadnej grupy łącznika pracy dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Rozwiąż problemy, które mogą wystąpić po nie pracy łącznika w grupie łącznika dla aplikacji z serwer Proxy aplikacji usługi Azure AD"
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
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="36577-103">Nie znaleziono aplikacji serwera Proxy aplikacji grupy łącznika pracy</span><span class="sxs-lookup"><span data-stu-id="36577-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="36577-104">Ten artykuł pomocy można rozwiązywać typowe problemy, które muszą ponieść gdy nie jest łącznika dla aplikacji serwera Proxy aplikacji wykryte zintegrowane z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36577-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="36577-105">Omówienie kroków</span><span class="sxs-lookup"><span data-stu-id="36577-105">Overview of steps</span></span>
<span data-ttu-id="36577-106">Jeśli nie ma żadnych pracy łącznika w grupie łącznika dla aplikacji, istnieje kilka sposobów, aby rozwiązać ten problem:</span><span class="sxs-lookup"><span data-stu-id="36577-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="36577-107">Jeśli nie łączniki do grupy, można:</span><span class="sxs-lookup"><span data-stu-id="36577-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="36577-108">Pobierz nowy łącznik na serwerze lokalnego prawo i przypisz je do tej grupy</span><span class="sxs-lookup"><span data-stu-id="36577-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="36577-109">Przenieś łącznika usługi active do grupy</span><span class="sxs-lookup"><span data-stu-id="36577-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="36577-110">Jeśli nie łączniki active w grupie, można:</span><span class="sxs-lookup"><span data-stu-id="36577-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="36577-111">Zidentyfikowanie przyczyny, dla której Twojego łącznika jest nieaktywny i rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="36577-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="36577-112">Przenieś łącznika usługi active do grupy</span><span class="sxs-lookup"><span data-stu-id="36577-112">Move an active Connector into the group</span></span>

<span data-ttu-id="36577-113">Aby wiedzieć, który z nich jest problem, otwórz menu "Serwer Proxy aplikacji" w aplikacji i przyjrzyj się komunikat ostrzegawczy grupy łącznika.</span><span class="sxs-lookup"><span data-stu-id="36577-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="36577-114">Określ go, że grupy wymaga co najmniej jeden łącznik (użytkownik nie masz żadnej grupy) lub że nie ma żadnych aktywnych łączników (Jeśli masz prawdopodobnie nieaktywne łączniki).</span><span class="sxs-lookup"><span data-stu-id="36577-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Wybór grupy łącznika w portalu Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="36577-116">Aby uzyskać szczegółowe informacje na każdej z tych opcji zobacz odpowiedniej sekcji poniżej.</span><span class="sxs-lookup"><span data-stu-id="36577-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="36577-117">Każdy z tych założono uruchamiasz na stronie zarządzania łącznika.</span><span class="sxs-lookup"><span data-stu-id="36577-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="36577-118">Jeśli jest wyświetlany komunikat o błędzie powyżej, można przejść do tej strony, klikając w komunikacie ostrzegawczym.</span><span class="sxs-lookup"><span data-stu-id="36577-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="36577-119">W przeciwnym razie to można znaleźć, przechodząc do **usługi Azure Active Directory**, klikając pozycję na **aplikacje dla przedsiębiorstw**, następnie **serwera Proxy aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="36577-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Łącznik grupy zarządzania w portalu Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="36577-121">Pobierz nowy łącznik</span><span class="sxs-lookup"><span data-stu-id="36577-121">Download a new Connector</span></span>

<span data-ttu-id="36577-122">Aby pobrać nowy łącznik, przycisk "Pobierz łącznik" w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="36577-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="36577-123">Uwaga łącznika musi być zainstalowany na komputerze z bezpośredniego procesów of wiersza do wewnętrznej bazy danych aplikacji i zwykle znajduje się na tym samym serwerze co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="36577-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="36577-124">Po pobraniu, łącznik powinna pojawić się w tym menu.</span><span class="sxs-lookup"><span data-stu-id="36577-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="36577-125">Kliknij łącznik i używając listy rozwijanej "łącznik grupy" Upewnij się, że należy on do grupy prawo.</span><span class="sxs-lookup"><span data-stu-id="36577-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="36577-126">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="36577-126">Save the change.</span></span>

   ![Pobierz łącznik z portalu Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="36577-128">Przenieś łącznika usługi Active</span><span class="sxs-lookup"><span data-stu-id="36577-128">Move an Active Connector</span></span>

<span data-ttu-id="36577-129">Jeśli masz łącznika usługi active powinna należeć do grupy i ma procesów z wiersza do zaplecza aplikacji docelowej, można przenieść łącznika w przypisanej grupie.</span><span class="sxs-lookup"><span data-stu-id="36577-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="36577-130">Aby to zrobić, kliknij przycisk łącznika.</span><span class="sxs-lookup"><span data-stu-id="36577-130">To do so, click the Connector.</span></span> <span data-ttu-id="36577-131">W polu "Łącznik grupy" Użyj listy rozwijanej wybierz poprawną grupę, a następnie kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="36577-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="36577-132">Rozwiąż nieaktywne łącznika</span><span class="sxs-lookup"><span data-stu-id="36577-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="36577-133">Jeśli nie są aktywne tylko łączników w grupie, prawdopodobnie na komputerze, na którym nie ma wszystkie niezbędne porty odblokowany.</span><span class="sxs-lookup"><span data-stu-id="36577-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="36577-134">znaleźć w dokumencie Rozwiązywanie problemów dotyczących portów szczegółowe badanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="36577-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36577-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36577-135">Next steps</span></span>
[<span data-ttu-id="36577-136">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="36577-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


