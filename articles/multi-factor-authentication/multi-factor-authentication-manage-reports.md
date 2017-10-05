---
title: "Raportów dotyczących dostępu i użycia dla usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Opisuje sposób użycia funkcji Azure Multi-Factor Authentication — raportów."
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
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="b790d-103">Raporty w uwierzytelnianie wieloskładnikowe platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b790d-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="b790d-104">Usługa Azure Multi-Factor Authentication udostępnia kilka raportów, które mogą być używane przez Ciebie i Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="b790d-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="b790d-105">Te raporty są dostępne za pośrednictwem portalu zarządzania usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="b790d-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="b790d-106">Poniżej przedstawiono listę dostępnych raportów:</span><span class="sxs-lookup"><span data-stu-id="b790d-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="b790d-107">Raport</span><span class="sxs-lookup"><span data-stu-id="b790d-107">Report</span></span> | <span data-ttu-id="b790d-108">Opis</span><span class="sxs-lookup"><span data-stu-id="b790d-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b790d-109">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="b790d-109">Usage</span></span> |<span data-ttu-id="b790d-110">Użycie raporty zawierają informacje na ogólne użycie, użytkownik Podsumowanie i szczegóły użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b790d-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="b790d-111">Stan serwera</span><span class="sxs-lookup"><span data-stu-id="b790d-111">Server Status</span></span> |<span data-ttu-id="b790d-112">Ten raport wyświetla stan serwerów usługi Multi-Factor Authentication skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="b790d-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="b790d-113">Historia zablokowanych użytkowników</span><span class="sxs-lookup"><span data-stu-id="b790d-113">Blocked User History</span></span> |<span data-ttu-id="b790d-114">Te raporty Pokaż historię żądań zablokowania lub odblokowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b790d-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="b790d-115">Historia pominiętych użytkowników</span><span class="sxs-lookup"><span data-stu-id="b790d-115">Bypassed User History</span></span> |<span data-ttu-id="b790d-116">Pokazuje historię żądań ominięcia usługi Multi-Factor Authentication dla użytkownika numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="b790d-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="b790d-117">Alert o oszustwie</span><span class="sxs-lookup"><span data-stu-id="b790d-117">Fraud Alert</span></span> |<span data-ttu-id="b790d-118">Wyświetla historię alertów oszustwa przesłanych w określonym zakresie daty.</span><span class="sxs-lookup"><span data-stu-id="b790d-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="b790d-119">W kolejce</span><span class="sxs-lookup"><span data-stu-id="b790d-119">Queued</span></span> |<span data-ttu-id="b790d-120">Prezentuje listę raportów w kolejce do przetwarzania i ich stan.</span><span class="sxs-lookup"><span data-stu-id="b790d-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="b790d-121">Po zakończeniu raportu zostanie podane łącze do pobrania lub wyświetlenia raportu.</span><span class="sxs-lookup"><span data-stu-id="b790d-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="b790d-122">Wyświetlanie raportów</span><span class="sxs-lookup"><span data-stu-id="b790d-122">View reports</span></span>
1. <span data-ttu-id="b790d-123">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b790d-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b790d-124">W obszarze po lewej stronie wybierz pozycję Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b790d-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="b790d-125">Wykonaj jedną z następujących dwóch opcji, w zależności od tego, czy używać dostawcy usługi MFA:</span><span class="sxs-lookup"><span data-stu-id="b790d-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="b790d-126">**Opcja 1**: kliknij kartę dostawców uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="b790d-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="b790d-127">Wybierz dostawcę uwierzytelniania MFA i kliknij przycisk **Zarządzaj** znajdujący się u dołu.</span><span class="sxs-lookup"><span data-stu-id="b790d-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="b790d-128">**Opcja 2**: Wybierz swój katalog, a następnie przejdź do **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="b790d-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="b790d-129">W sekcji uwierzytelniania wieloskładnikowego wybierz pozycję **Zarządzaj ustawieniami usługi**.</span><span class="sxs-lookup"><span data-stu-id="b790d-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="b790d-130">Na dole strony Ustawienia usługi MFA, kliknij polecenie Przejdź do portalu łącza.</span><span class="sxs-lookup"><span data-stu-id="b790d-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="b790d-131">W portalu zarządzania Azure Multi-Factor Authentication należy wybrać typ raportu z **wyświetlić raport** sekcji na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="b790d-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="b790d-132"><center>![Chmura](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="b790d-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="b790d-133">**Dodatkowe zasoby**</span><span class="sxs-lookup"><span data-stu-id="b790d-133">**Additional Resources**</span></span>

* [<span data-ttu-id="b790d-134">Dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="b790d-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="b790d-135">Usługa Azure Multi-Factor Authentication w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="b790d-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
