---
title: "Jak używać dostęp do aplikacji Sklep internetowy | Dokumentacja firmy Microsoft"
description: "Włącz dostęp do aplikacji Sklep internetowy umożliwia użytkownikom znajdowanie własne aplikacje"
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
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="251c5-103">Jak używać dostęp do aplikacji Sklep internetowy</span><span class="sxs-lookup"><span data-stu-id="251c5-103">How to use self-service application access</span></span>

<span data-ttu-id="251c5-104">Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy włączyć **dostęp do aplikacji Sklep internetowy** do dowolnych aplikacji, które chcesz zezwolić użytkownikom na własnym odnajdywania i żądania dostępu do.</span><span class="sxs-lookup"><span data-stu-id="251c5-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="251c5-105">Ta funkcja jest to doskonały sposób, można oszczędzić czas i pieniądze jako grupa IT i zdecydowanie zaleca się jako część wdrożenia nowoczesnych aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="251c5-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="251c5-106">Za pomocą tej funkcji, można:</span><span class="sxs-lookup"><span data-stu-id="251c5-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="251c5-107">Zezwala użytkownikom na własnym odnajdywanie aplikacji z [panelu dostępu aplikacji](https://myapps.microsoft.com/) bez bothering grupę IT.</span><span class="sxs-lookup"><span data-stu-id="251c5-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="251c5-108">Dodaj tych użytkowników do wstępnie skonfigurowanej grupy, aby zobaczyć, kto żąda dostępu, usunięcie dostępu i zarządzanie rolami do nich przypisane.</span><span class="sxs-lookup"><span data-stu-id="251c5-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="251c5-109">Opcjonalnie zezwolić osoba zatwierdzająca biznesowych do zatwierdzenia żądania dostępu do aplikacji, nie ma grupa IT.</span><span class="sxs-lookup"><span data-stu-id="251c5-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="251c5-110">Opcjonalnie można skonfigurować maksymalnie 10 użytkowników indywidualnych, którzy mogą zatwierdzić dostęp do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="251c5-111">Opcjonalnie zezwolić firma osoba zatwierdzająca Ustaw hasła użytkowników można użyć do logowania do aplikacji, z biznesowe osoby zatwierdzającej [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="251c5-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="251c5-112">Opcjonalnie automatycznie przypisywać samoobsługi bezpośrednio przypisać użytkowników do roli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="251c5-113">Włącz dostęp do aplikacji Sklep internetowy umożliwia użytkownikom znajdowanie własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="251c5-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="251c5-114">Dostęp do aplikacji Sklep internetowy jest to dobry sposób, aby zezwolić użytkownikom na własnym odnajdywanie aplikacji, opcjonalnie zezwolić grupie biznesowej, aby zatwierdzić dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="251c5-115">Możesz zezwolić grupie biznesowej do zarządzania poświadczeniami przypisane do tych użytkowników do prawej jednokrotnego hasła w aplikacji z ich paneli dostępu.</span><span class="sxs-lookup"><span data-stu-id="251c5-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="251c5-116">Aby włączyć samoobsługowe aplikacji dostęp do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="251c5-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="251c5-117">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="251c5-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="251c5-118">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="251c5-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="251c5-119">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="251c5-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="251c5-120">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="251c5-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="251c5-121">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="251c5-122">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="251c5-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="251c5-123">Wybierz aplikację, aby umożliwić samoobsługi dostęp do z listy.</span><span class="sxs-lookup"><span data-stu-id="251c5-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="251c5-124">Po załadowaniu aplikacji, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="251c5-125">Aby włączyć dostęp do aplikacji Sklep internetowy dla tej aplikacji, należy włączyć **Zezwalaj użytkownikom na żądanie dostępu do tej aplikacji?** Przełącz, aby **tak.**</span><span class="sxs-lookup"><span data-stu-id="251c5-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="251c5-126">Następnie wybierz grupę, do których użytkownicy, którzy żądają dostępu do tej aplikacji można dodać, kliknij przycisk wyboru obok etykiety **do grupy, do której ma zostać dodany przypisanych użytkowników?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="251c5-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="251c5-127">**Opcjonalnie:** aby wymagają zatwierdzenia biznesowych, przed użytkownicy mają dostęp, ustaw **wymagają zatwierdzenia przed udzieleniem im dostępu do tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="251c5-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="251c5-128">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** Jeśli chcesz umożliwić tych osób zatwierdzających firm określić hasła, które są wysyłane do tej aplikacji dla zatwierdzonych użytkowników, ustawić **Zezwalaj osób zatwierdzających można ustawić hasła użytkownika dla tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="251c5-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="251c5-129">**Opcjonalnie:** do określenia osób zatwierdzających biznesowych, którzy mogą zatwierdzić dostęp do tej aplikacji, kliknij przycisk wyboru obok etykiety **kto może zatwierdzić dostęp do tej aplikacji?** wybrać maksymalnie 10 firm poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="251c5-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="251c5-130">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="251c5-130">Groups are not supported.</span></span>

13. <span data-ttu-id="251c5-131">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz przypisać do roli użytkowników samoobsługi zatwierdzone, kliknij selektor **do roli należy użytkowników można przypisać w tej aplikacji?** wybierz rolę, do której można przypisać tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="251c5-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="251c5-132">Kliknij przycisk **zapisać** na górze bloku, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="251c5-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="251c5-133">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić do ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk **+ Dodaj** przycisk, aby znaleźć aplikacji, dla których włączono samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="251c5-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="251c5-134">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="251c5-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="251c5-135">Można włączyć wiadomość e-mail z informacją, gdy użytkownik żąda dostępu do aplikacji, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="251c5-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="251c5-136">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że jeśli określisz wiele osób zatwierdzających żadnych jedna osoba zatwierdzająca może zatwierdzić dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251c5-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="251c5-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="251c5-137">Next steps</span></span>
[<span data-ttu-id="251c5-138">Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi</span><span class="sxs-lookup"><span data-stu-id="251c5-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
