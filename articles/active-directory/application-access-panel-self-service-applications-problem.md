---
title: "Problem za pomocą dostępu do aplikacji Sklep internetowy | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów związanych z dostępem do aplikacji Sklep internetowy do"
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
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="3bce7-103">Problem za pomocą dostępu do aplikacji Sklep internetowy</span><span class="sxs-lookup"><span data-stu-id="3bce7-103">Problem using self-service application access</span></span>

<span data-ttu-id="3bce7-104">Dostęp do aplikacji Sklep internetowy jest to dobry sposób, aby zezwolić użytkownikom na własnym odnajdywanie aplikacji, opcjonalnie zezwolić grupie biznesowej, aby zatwierdzić dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bce7-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="3bce7-105">Możesz zezwolić grupie biznesowej do zarządzania poświadczeniami przypisane do tych użytkowników do prawej jednokrotnego hasła w aplikacji z ich paneli dostępu.</span><span class="sxs-lookup"><span data-stu-id="3bce7-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="3bce7-106">Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy włączyć **dostęp do aplikacji Sklep internetowy** do dowolnych aplikacji, które chcesz zezwolić użytkownikom na własnym odnajdywania i żądania dostępu do.</span><span class="sxs-lookup"><span data-stu-id="3bce7-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="3bce7-107">Ogólne problemy, aby sprawdzić w pierwszej kolejności</span><span class="sxs-lookup"><span data-stu-id="3bce7-107">General issues to check first</span></span>

-   <span data-ttu-id="3bce7-108">Upewnij się, że poprawnie skonfigurowano dostęp do aplikacji Sklep internetowy.</span><span class="sxs-lookup"><span data-stu-id="3bce7-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="3bce7-109">Zobacz sekcję "Jak skonfigurować dostęp do aplikacji Sklep internetowy".</span><span class="sxs-lookup"><span data-stu-id="3bce7-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="3bce7-110">Upewnij się, że włączono użytkownika lub grupy, aby zażądać dostępu do aplikacji Sklep internetowy.</span><span class="sxs-lookup"><span data-stu-id="3bce7-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="3bce7-111">Upewnij się, że użytkownik jest odwiedzający odpowiednie miejsce dostępu do aplikacji Sklep internetowy.</span><span class="sxs-lookup"><span data-stu-id="3bce7-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="3bce7-112">Użytkownicy mogą przechodzić do ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk **+ Dodaj** przycisk, aby znaleźć aplikacji, dla których włączono samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="3bce7-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="3bce7-113">Jeśli dostęp do aplikacji Sklep internetowy niedawno została skonfigurowana, spróbuj logowanie i wylogowywanie ponownie do panelu dostępu użytkownika po kilku minutach się jeśli zmian dostępu samoobsługi pojawiły się w temacie.</span><span class="sxs-lookup"><span data-stu-id="3bce7-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="3bce7-114">Jak skonfigurować dostęp do aplikacji Sklep internetowy</span><span class="sxs-lookup"><span data-stu-id="3bce7-114">How to configure self-service application access</span></span>

<span data-ttu-id="3bce7-115">Aby włączyć samoobsługowe aplikacji dostęp do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3bce7-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="3bce7-116">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="3bce7-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3bce7-117">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="3bce7-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3bce7-118">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="3bce7-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3bce7-119">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bce7-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3bce7-120">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bce7-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3bce7-121">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="3bce7-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3bce7-122">Wybierz aplikację, aby umożliwić samoobsługi dostęp do z listy.</span><span class="sxs-lookup"><span data-stu-id="3bce7-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="3bce7-123">Po załadowaniu aplikacji, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bce7-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3bce7-124">Aby włączyć dostęp do aplikacji Sklep internetowy dla tej aplikacji, należy włączyć **Zezwalaj użytkownikom na żądanie dostępu do tej aplikacji?** Przełącz, aby **tak.**</span><span class="sxs-lookup"><span data-stu-id="3bce7-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="3bce7-125">Następnie wybierz grupę, do których użytkownicy, którzy żądają dostępu do tej aplikacji można dodać, kliknij przycisk wyboru obok etykiety **do grupy, do której ma zostać dodany przypisanych użytkowników?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="3bce7-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="3bce7-126">**Opcjonalnie:** aby wymagają zatwierdzenia biznesowych, przed użytkownicy mają dostęp, ustaw **wymagają zatwierdzenia przed udzieleniem im dostępu do tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="3bce7-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="3bce7-127">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** Jeśli chcesz umożliwić tych osób zatwierdzających firm określić hasła, które są wysyłane do tej aplikacji dla zatwierdzonych użytkowników, ustawić **Zezwalaj osób zatwierdzających można ustawić hasła użytkownika dla tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="3bce7-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="3bce7-128">**Opcjonalnie:** do określenia osób zatwierdzających biznesowych, którzy mogą zatwierdzić dostęp do tej aplikacji, kliknij przycisk wyboru obok etykiety **kto może zatwierdzić dostęp do tej aplikacji?** wybrać maksymalnie 10 firm poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="3bce7-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="3bce7-129">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3bce7-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="3bce7-130">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz przypisać do roli użytkowników samoobsługi zatwierdzone, kliknij selektor **do roli należy użytkowników można przypisać w tej aplikacji?** wybierz rolę, do której można przypisać tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3bce7-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="3bce7-131">Kliknij przycisk **zapisać** na górze bloku, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="3bce7-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="3bce7-132">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić do ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk **+ Dodaj** przycisk, aby znaleźć aplikacji, dla których włączono samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="3bce7-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="3bce7-133">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3bce7-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="3bce7-134">Można włączyć wiadomość e-mail z informacją, gdy użytkownik żąda dostępu do aplikacji, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="3bce7-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="3bce7-135">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że jeśli określisz wiele osób zatwierdzających żadnych jedna osoba zatwierdzająca może zatwierdzić dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bce7-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="3bce7-136">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu</span><span class="sxs-lookup"><span data-stu-id="3bce7-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="3bce7-137">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="3bce7-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="3bce7-138">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="3bce7-138">Correlation error ID</span></span>

-   <span data-ttu-id="3bce7-139">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="3bce7-139">UPN (user email address)</span></span>

-   <span data-ttu-id="3bce7-140">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="3bce7-140">TenantID</span></span>

-   <span data-ttu-id="3bce7-141">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="3bce7-141">Browser type</span></span>

-   <span data-ttu-id="3bce7-142">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="3bce7-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3bce7-143">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="3bce7-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bce7-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bce7-144">Next steps</span></span>
[<span data-ttu-id="3bce7-145">Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi</span><span class="sxs-lookup"><span data-stu-id="3bce7-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
