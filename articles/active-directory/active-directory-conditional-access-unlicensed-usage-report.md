---
title: "Raport użycia licencji | Dokumentacja firmy Microsoft"
description: "Pomaga raport użycia licencji zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD."
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
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="4d528-103">Raport użycia licencji</span><span class="sxs-lookup"><span data-stu-id="4d528-103">Unlicensed usage report</span></span>
<span data-ttu-id="4d528-104">Pomaga raport użycia licencji zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d528-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="4d528-105">Dzięki temu można ulepszyć użycie licencji, które zostały zakupione i do identyfikowania wiadomo, kiedy może być konieczne dodatkowe licencje.</span><span class="sxs-lookup"><span data-stu-id="4d528-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="4d528-106">Ten raport prezentuje active użycie płatnych funkcji w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="4d528-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="4d528-107">Struktura raportu</span><span class="sxs-lookup"><span data-stu-id="4d528-107">Report structure</span></span>
| <span data-ttu-id="4d528-108">Nazwa kolumny</span><span class="sxs-lookup"><span data-stu-id="4d528-108">Column name</span></span> | <span data-ttu-id="4d528-109">Opis</span><span class="sxs-lookup"><span data-stu-id="4d528-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d528-110">Bez licencji użytkownika</span><span class="sxs-lookup"><span data-stu-id="4d528-110">Unlicensed User</span></span> |<span data-ttu-id="4d528-111">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="4d528-111">Name of the user</span></span> |
| <span data-ttu-id="4d528-112">Funkcja</span><span class="sxs-lookup"><span data-stu-id="4d528-112">Feature</span></span> |<span data-ttu-id="4d528-113">Nazwa funkcji.</span><span class="sxs-lookup"><span data-stu-id="4d528-113">The feature name.</span></span> <span data-ttu-id="4d528-114">Na przykład: dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="4d528-114">For example: conditional access</span></span> |
| <span data-ttu-id="4d528-115">Dostęp do aplikacji</span><span class="sxs-lookup"><span data-stu-id="4d528-115">Application Accessed</span></span> |<span data-ttu-id="4d528-116">Nazwa aplikacji, która jest uzyskiwany z funkcją.</span><span class="sxs-lookup"><span data-stu-id="4d528-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="4d528-117">Na przykład: usługi Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4d528-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="4d528-118">Jeśli konto użytkownika zostało usunięte zostaną wypełnione kolumny "Bez licencji użytkownika" z Identyfikatorem, takich jak 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="4d528-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="4d528-119">Funkcja dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="4d528-119">Conditional access feature</span></span>
<span data-ttu-id="4d528-120">Nielicencjonowani użytkownicy zostaną oflagowane przy uzyskiwaniu dostępu do usługi, która ma zasady dostępu warunkowego zastosowane, jeśli nie mają licencji usługi Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="4d528-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="4d528-121">Dotyczy to usługi MFA / zasady lokalizacji, a także urządzenia zasady korzystające z usługi Intune.</span><span class="sxs-lookup"><span data-stu-id="4d528-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="4d528-122">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4d528-122">See also</span></span>
* [<span data-ttu-id="4d528-123">Za pomocą dostępu warunkowego z usługą Office 365 i inne usługi Azure Active Directory podłączonego aplikacji</span><span class="sxs-lookup"><span data-stu-id="4d528-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="4d528-124">Wprowadzenie do korzystania z dostępu warunkowego do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d528-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

