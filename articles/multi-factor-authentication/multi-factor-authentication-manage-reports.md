---
title: "raportów aaaAccess i użycia dla usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse hello funkcji Azure Multi-Factor Authentication — raportów."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="54e36-103">Raporty w uwierzytelnianie wieloskładnikowe platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54e36-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="54e36-104">Usługa Azure Multi-Factor Authentication udostępnia kilka raportów, które mogą być używane przez Ciebie i Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="54e36-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="54e36-105">Te raporty są dostępne za pośrednictwem hello Portal zarządzania usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="54e36-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="54e36-106">Witaj poniżej przedstawiono listę dostępnych raportów hello:</span><span class="sxs-lookup"><span data-stu-id="54e36-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="54e36-107">Raport</span><span class="sxs-lookup"><span data-stu-id="54e36-107">Report</span></span> | <span data-ttu-id="54e36-108">Opis</span><span class="sxs-lookup"><span data-stu-id="54e36-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="54e36-109">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="54e36-109">Usage</span></span> |<span data-ttu-id="54e36-110">Użycie Hello raporty zawierają informacje na ogólne użycie, użytkownik Podsumowanie i szczegóły użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54e36-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="54e36-111">Stan serwera</span><span class="sxs-lookup"><span data-stu-id="54e36-111">Server Status</span></span> |<span data-ttu-id="54e36-112">Ten raport wyświetla stan hello serwerów usługi Multi-Factor Authentication skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="54e36-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="54e36-113">Historia zablokowanych użytkowników</span><span class="sxs-lookup"><span data-stu-id="54e36-113">Blocked User History</span></span> |<span data-ttu-id="54e36-114">Te raporty Pokaż historię hello tooblock żądania lub odblokowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="54e36-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="54e36-115">Historia pominiętych użytkowników</span><span class="sxs-lookup"><span data-stu-id="54e36-115">Bypassed User History</span></span> |<span data-ttu-id="54e36-116">Przedstawia historię hello toobypass żądań uwierzytelniania wieloskładnikowego dla użytkownika numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="54e36-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="54e36-117">Alert o oszustwie</span><span class="sxs-lookup"><span data-stu-id="54e36-117">Fraud Alert</span></span> |<span data-ttu-id="54e36-118">Wyświetla historię alertów oszustwa przesłanych w określonym zakresie daty hello.</span><span class="sxs-lookup"><span data-stu-id="54e36-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="54e36-119">W kolejce</span><span class="sxs-lookup"><span data-stu-id="54e36-119">Queued</span></span> |<span data-ttu-id="54e36-120">Prezentuje listę raportów w kolejce do przetwarzania i ich stan.</span><span class="sxs-lookup"><span data-stu-id="54e36-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="54e36-121">Po zakończeniu raportu hello stosownym raporcie hello toodownload lub widok łącza.</span><span class="sxs-lookup"><span data-stu-id="54e36-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="54e36-122">Wyświetlanie raportów</span><span class="sxs-lookup"><span data-stu-id="54e36-122">View reports</span></span>
1. <span data-ttu-id="54e36-123">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="54e36-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="54e36-124">Po lewej stronie powitania wybierz usługę Active Directory.</span><span class="sxs-lookup"><span data-stu-id="54e36-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="54e36-125">Wykonaj jedną z następujących dwóch opcji, w zależności od tego, czy używać dostawcy usługi MFA:</span><span class="sxs-lookup"><span data-stu-id="54e36-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="54e36-126">**Opcja 1**: hello kartę dostawców uwierzytelniania wieloskładnikowego. Wybierz dostawcę uwierzytelniania MFA, a następnie kliknij przycisk hello **Zarządzaj** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="54e36-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="54e36-127">**Opcja 2**: Wybierz toohello Twojego katalogu i Przejdź **Konfiguruj** kartę. W sekcji uwierzytelnianie wieloskładnikowe hello, wybierz **Zarządzaj ustawieniami usługi**.</span><span class="sxs-lookup"><span data-stu-id="54e36-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="54e36-128">U dołu hello hello strony Ustawienia usługi MFA kliknij przycisk hello Przejdź toohello portalu łącza.</span><span class="sxs-lookup"><span data-stu-id="54e36-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="54e36-129">W portalu zarządzania Azure Multi-Factor Authentication hello, wybierz typ hello z raportu ma hello **wyświetlić raport** części hello lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="54e36-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="54e36-130"><center>![Chmura](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="54e36-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="54e36-131">**Dodatkowe zasoby**</span><span class="sxs-lookup"><span data-stu-id="54e36-131">**Additional Resources**</span></span>

* [<span data-ttu-id="54e36-132">Dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="54e36-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="54e36-133">Usługa Azure Multi-Factor Authentication w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="54e36-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
