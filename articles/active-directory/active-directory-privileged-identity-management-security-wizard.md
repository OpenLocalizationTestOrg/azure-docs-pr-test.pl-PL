---
title: "Kreator zabezpieczeń usługi Azure AD Privileged Identity Management"
description: "Użyj rozszerzenia usługi Azure Active Directory Privileged Identity Management po raz pierwszy zostanie wyświetlona za pomocą Kreatora zabezpieczeń. W tym artykule opisano kroki dotyczące korzystania z kreatora."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="218ed-104">Za pomocą Kreatora zabezpieczeń w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="218ed-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="218ed-105">Jeśli jesteś pierwszą osobą, która Uruchom Azure Privileged Identity zarządzania (PIM) dla organizacji, użytkownik zobaczy za pomocą kreatora.</span><span class="sxs-lookup"><span data-stu-id="218ed-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="218ed-106">Kreator pomaga w zrozumieniu zagrożenia bezpieczeństwa tożsamości uprzywilejowanych oraz sposobu używania usługi PIM te zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="218ed-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="218ed-107">Nie trzeba wprowadzać żadnych zmian w istniejących przypisań ról w kreatorze, aby zrobić to później.</span><span class="sxs-lookup"><span data-stu-id="218ed-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="218ed-108">Czego oczekiwać</span><span class="sxs-lookup"><span data-stu-id="218ed-108">What to expect</span></span>
<span data-ttu-id="218ed-109">Przed rozpoczęciem organizacji przy użyciu usługi PIM są trwałe, wszystkie przypisania roli: użytkownicy są zawsze w ramach tych ról, nawet jeśli ich nie są obecnie wymagane ich uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="218ed-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="218ed-110">Pierwszy krok kreatora zawiera listę ról z wysokim poziomem i ilu użytkowników aktualnie znajdują się w tych ról.</span><span class="sxs-lookup"><span data-stu-id="218ed-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="218ed-111">Można przejść do określonej roli, aby uzyskać więcej informacji użytkowników, jeśli jeden lub jeden z nich jest nieznane.</span><span class="sxs-lookup"><span data-stu-id="218ed-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="218ed-112">Drugim kroku kreatora daje możliwość zmiany przypisań ról administratora.</span><span class="sxs-lookup"><span data-stu-id="218ed-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="218ed-113">Jest ważne, czy masz co najmniej jednego administratora globalnego i więcej niż jeden administrator ról uprzywilejowanych za pomocą konta organizacyjnego (a nie kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="218ed-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="218ed-114">Jeśli istnieje tylko jeden administrator ról uprzywilejowanych, organizacji, nie będzie mógł zarządzać PIM usunięcie tego konta.</span><span class="sxs-lookup"><span data-stu-id="218ed-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="218ed-115">Ponadto przypisań ról Zachowaj stałe, jeśli użytkownik ma konto Microsoft (konta używanego do logowania do usług firmy Microsoft, takich jak Skype i Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="218ed-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="218ed-116">Jeśli planujesz wymagają usługi MFA do aktywacji dla tej roli użytkownika zostanie zablokowane.</span><span class="sxs-lookup"><span data-stu-id="218ed-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="218ed-117">Po dokonaniu zmian, Kreator będzie już wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="218ed-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="218ed-118">Następnym razem, użytkownik lub inny administrator ról uprzywilejowanych używać aplikacji PIM, zostanie wyświetlony pulpit nawigacyjny usługi PIM.</span><span class="sxs-lookup"><span data-stu-id="218ed-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="218ed-119">Jeśli chcesz dodać lub usunąć użytkowników z ról lub zmienić przypisania z stałe kwalifikujących się Dowiedz się więcej o [jak dodać lub usunąć rolę użytkownika](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="218ed-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="218ed-120">Jeśli chcesz umożliwić użytkownikom więcej dostęp do zarządzania PIM, Dowiedz się więcej o [sposób udzielić dostępu do zarządzania w PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="218ed-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="218ed-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="218ed-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

