---
title: "Raport użycia aaaUnlicensed | Dokumentacja firmy Microsoft"
description: "Witaj raportu użycia licencji, które pomaga zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="7a179-103">Raport użycia licencji</span><span class="sxs-lookup"><span data-stu-id="7a179-103">Unlicensed usage report</span></span>
<span data-ttu-id="7a179-104">Witaj raportu użycia licencji, które pomaga zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a179-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="7a179-105">Dzięki temu można lepiej wykorzystać toomake licencji, które zostały zakupione i tooidentify wiedzieć, kiedy użytkownik może być konieczne dodatkowe licencje.</span><span class="sxs-lookup"><span data-stu-id="7a179-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="7a179-106">przedstawia Hello active użycie hello płatnej funkcje w hello w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="7a179-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="7a179-107">Struktura raportu</span><span class="sxs-lookup"><span data-stu-id="7a179-107">Report structure</span></span>
| <span data-ttu-id="7a179-108">Nazwa kolumny</span><span class="sxs-lookup"><span data-stu-id="7a179-108">Column name</span></span> | <span data-ttu-id="7a179-109">Opis</span><span class="sxs-lookup"><span data-stu-id="7a179-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a179-110">Bez licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="7a179-110">Unlicensed User</span></span> |<span data-ttu-id="7a179-111">Nazwa użytkownika, powitalne</span><span class="sxs-lookup"><span data-stu-id="7a179-111">Name of hello user</span></span> |
| <span data-ttu-id="7a179-112">Funkcja</span><span class="sxs-lookup"><span data-stu-id="7a179-112">Feature</span></span> |<span data-ttu-id="7a179-113">Nazwa funkcji Hello.</span><span class="sxs-lookup"><span data-stu-id="7a179-113">hello feature name.</span></span> <span data-ttu-id="7a179-114">Na przykład: dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="7a179-114">For example: conditional access</span></span> |
| <span data-ttu-id="7a179-115">Dostęp do aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a179-115">Application Accessed</span></span> |<span data-ttu-id="7a179-116">Nazwa Hello aplikacji hello, która jest uzyskiwany za pomocą funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="7a179-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="7a179-117">Na przykład: usługi Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7a179-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="7a179-118">Jeśli konto użytkownika zostało usunięte Witaj "Bez licencji użytkownika" zostaną wypełnione kolumny o identyfikatorze, takich jak 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="7a179-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="7a179-119">Funkcja dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="7a179-119">Conditional access feature</span></span>
<span data-ttu-id="7a179-120">Nielicencjonowani użytkownicy zostaną oflagowane przy uzyskiwaniu dostępu do usługi, która ma zasady dostępu warunkowego zastosowane, jeśli nie mają licencji usługi Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="7a179-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="7a179-121">Dotyczy to tooMFA / zasady lokalizacji, a także urządzenia zasady, które przy użyciu usługi Intune.</span><span class="sxs-lookup"><span data-stu-id="7a179-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="7a179-122">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7a179-122">See also</span></span>
* [<span data-ttu-id="7a179-123">Za pomocą dostępu warunkowego z usługą Office 365 i inne usługi Azure Active Directory podłączonego aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a179-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="7a179-124">Wprowadzenie do korzystania z dostępu warunkowego tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="7a179-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

