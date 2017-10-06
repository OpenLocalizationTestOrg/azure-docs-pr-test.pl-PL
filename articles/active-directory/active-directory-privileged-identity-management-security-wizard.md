---
title: "Kreator zabezpieczeń aaaThe usługi Azure AD Privileged Identity Management"
description: "Witaj po raz pierwszy używasz rozszerzenia usługi Azure Active Directory Privileged Identity Management hello, zostanie wyświetlona za pomocą Kreatora zabezpieczeń. W tym artykule opisano kroki hello za pomocą Kreatora hello."
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="e4dd1-104">Za pomocą Kreatora zabezpieczeń hello w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e4dd1-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="e4dd1-105">Jeśli pierwszy toorun osoby hello Azure Privileged Identity zarządzania (PIM) dla organizacji, użytkownik zobaczy za pomocą kreatora.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="e4dd1-106">Kreator Hello pomaga w zrozumieniu hello zagrożeniach związanych z tożsamościami uprzywilejowanymi i w jaki sposób toouse PIM tooreduce tych zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="e4dd1-107">Nie ma potrzeby toomake przypisań ról tooexisting wszelkie zmiany w Kreatorze hello, jeśli wolisz toodo go później.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="e4dd1-108">Jakie tooexpect</span><span class="sxs-lookup"><span data-stu-id="e4dd1-108">What tooexpect</span></span>
<span data-ttu-id="e4dd1-109">Przed rozpoczęciem organizacji przy użyciu usługi PIM są trwałe, wszystkie przypisania roli: hello użytkownicy są zawsze w ramach tych ról, nawet jeśli ich nie są obecnie wymagane ich uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="e4dd1-110">pierwszym krokiem Hello kreatora hello zawiera listę ról z wysokim poziomem i ilu użytkowników aktualnie znajdują się w tych ról.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="e4dd1-111">Można przejść w toolearn określoną rolę tooa więcej informacji na temat użytkowników, jeśli co najmniej jedna z nich jest nieznane.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="e4dd1-112">drugim kroku kreatora hello Hello daje administrator toochange możliwość przypisania ról.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="e4dd1-113">Jest ważne, czy masz co najmniej jednego administratora globalnego i więcej niż jeden administrator ról uprzywilejowanych za pomocą konta organizacyjnego (a nie kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e4dd1-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="e4dd1-114">Jeśli istnieje tylko jeden administrator ról uprzywilejowanych, hello organizacji nie będą mogli toomanage PIM usunięcie tego konta.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="e4dd1-115">Ponadto przypisań ról Zachowaj stałe, jeśli użytkownik ma konto Microsoft (konto się, że używają one toosign w tooMicrosoft usług takich jak Skype i Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="e4dd1-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="e4dd1-116">Jeśli planujesz toorequire MFA do aktywacji dla tej roli użytkownika zostanie zablokowane.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="e4dd1-117">Po dokonaniu zmian, Kreator hello będą już widoczne.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="e4dd1-118">Witaj następnym razem, użytkownik lub inny administrator ról uprzywilejowanych używać aplikacji PIM, zostanie wyświetlony pulpit nawigacyjny PIM hello.</span><span class="sxs-lookup"><span data-stu-id="e4dd1-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="e4dd1-119">Czy tooadd, takich jak lub usuwać użytkowników z ról lub zmiana przypisania z tooeligible stałe, Dowiedz się więcej o [jak tooadd lub usunąć rolę użytkownika](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="e4dd1-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="e4dd1-120">Jeśli chcesz toogive więcej użytkownicy uzyskują dostęp do toomanage PIM, Dowiedz się więcej o [jak toogive dostępu toomanage w PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="e4dd1-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4dd1-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4dd1-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

