---
title: "Jak przypisać użytkowników i grup do aplikacji | Dokumentacja firmy Microsoft"
description: "Przypisywanie użytkowników do aplikacji w celu udzielenia dostępu"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="b386b-103">Jak przypisać użytkowników i grup do aplikacji</span><span class="sxs-lookup"><span data-stu-id="b386b-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="b386b-104">Zanim użytkownicy mogą wykonać żadnej z poniżej dla określonej aplikacji, musisz najpierw **przypisać je do aplikacji** Aby udzielić im dostępu:</span><span class="sxs-lookup"><span data-stu-id="b386b-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="b386b-105">Uzyskiwanie dostępu do aplikacji przez **nawigowanie do adresu URL aplikacji bezpośrednio** (nazywany także inicjowane SP logowania jednokrotnego).</span><span class="sxs-lookup"><span data-stu-id="b386b-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="b386b-106">Dostęp do aplikacji przy użyciu **adres URL dostępu użytkownika** w aplikacji **właściwości** strony (nazywany także inicjowane IDP logowania).</span><span class="sxs-lookup"><span data-stu-id="b386b-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="b386b-107">Zobacz aplikacji są wyświetlane na ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="b386b-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="b386b-108">Zobacz aplikacji są wyświetlane na ich [uruchamiający aplikację usługi Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="b386b-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="b386b-109">Metody przypisania aplikacji za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b386b-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="b386b-110">Istnieją 3 sposoby można przypisać aplikacji za pomocą usługi Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="b386b-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="b386b-111">Przypisywanie użytkownika bezpośrednio do aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="b386b-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="b386b-112">Przypisz grupę bezpośrednio do aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="b386b-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="b386b-113">Włącz dostęp do aplikacji Sklep internetowy umożliwia użytkownikom znajdowanie własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="b386b-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="b386b-114">Przypisywanie użytkownika bezpośrednio jako administrator</span><span class="sxs-lookup"><span data-stu-id="b386b-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="b386b-115">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b386b-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b386b-116">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="b386b-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b386b-117">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b386b-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b386b-118">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b386b-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b386b-119">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b386b-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b386b-120">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b386b-121">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="b386b-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b386b-122">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b386b-123">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b386b-124">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="b386b-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b386b-125">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="b386b-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b386b-126">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b386b-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b386b-127">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="b386b-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b386b-128">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b386b-129">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="b386b-130">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b386b-131">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="b386b-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="b386b-132">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b386b-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="b386b-133">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji za pomocą metod opisanych w sekcji Opis rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b386b-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="b386b-134">Przypisz grupę bezpośrednio do aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="b386b-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="b386b-135">Aby przypisać co najmniej jedną grupę aplikacji bezpośrednio, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b386b-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b386b-136">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="b386b-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b386b-137">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b386b-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b386b-138">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b386b-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b386b-139">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b386b-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b386b-140">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b386b-141">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="b386b-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b386b-142">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b386b-143">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b386b-144">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="b386b-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b386b-145">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="b386b-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b386b-146">Wpisz w **grupy Pełna nazwa** planuje się przypisanie do grupy **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b386b-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b386b-147">Umieść kursor nad **grupy** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="b386b-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b386b-148">Kliknij pole wyboru obok profilu zdjęcie lub logo, aby dodać użytkownika do grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b386b-149">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jedną grupę**, typu w innym **grupy Pełna nazwa** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać tę grupę do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="b386b-150">Po wybraniu grup kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b386b-151">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="b386b-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="b386b-152">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="b386b-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="b386b-153">Po krótkim czasie użytkowników w grupach, który wybrano mieć możliwość uruchamiania tych aplikacji za pomocą metod opisanych w sekcji Opis rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b386b-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="b386b-154">Jeśli są one grup dynamicznych, mogą występować pewne opóźnienie dodatkowego przetwarzania w tych przydziałów dla użytkowników w tych przypisanych grup.</span><span class="sxs-lookup"><span data-stu-id="b386b-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="b386b-155">Włącz dostęp do aplikacji Sklep internetowy umożliwia użytkownikom znajdowanie własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="b386b-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="b386b-156">Dostęp do aplikacji Sklep internetowy jest to dobry sposób, aby zezwolić użytkownikom na własnym odnajdywanie aplikacji, opcjonalnie zezwolić grupie biznesowej, aby zatwierdzić dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="b386b-157">Możesz zezwolić grupie biznesowej do zarządzania poświadczeniami przypisane do tych użytkowników do prawej jednokrotnego hasła w aplikacji z ich paneli dostępu.</span><span class="sxs-lookup"><span data-stu-id="b386b-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="b386b-158">Aby włączyć samoobsługowe aplikacji dostęp do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b386b-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="b386b-159">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="b386b-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b386b-160">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b386b-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b386b-161">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b386b-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b386b-162">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b386b-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b386b-163">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b386b-164">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="b386b-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b386b-165">Wybierz aplikację, aby umożliwić samoobsługi dostęp do z listy.</span><span class="sxs-lookup"><span data-stu-id="b386b-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="b386b-166">Po załadowaniu aplikacji, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b386b-167">Aby włączyć dostęp do aplikacji Sklep internetowy dla tej aplikacji, należy włączyć **Zezwalaj użytkownikom na żądanie dostępu do tej aplikacji?** Przełącz, aby **tak.**</span><span class="sxs-lookup"><span data-stu-id="b386b-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="b386b-168">Następnie wybierz grupę, do których użytkownicy, którzy żądają dostępu do tej aplikacji można dodać, kliknij przycisk wyboru obok etykiety **do grupy, do której ma zostać dodany przypisanych użytkowników?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="b386b-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="b386b-169">**Opcjonalnie:** aby wymagają zatwierdzenia biznesowych, przed użytkownicy mają dostęp, ustaw **wymagają zatwierdzenia przed udzieleniem im dostępu do tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="b386b-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="b386b-170">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** Jeśli chcesz umożliwić tych osób zatwierdzających firm określić hasła, które są wysyłane do tej aplikacji dla zatwierdzonych użytkowników, ustawić **Zezwalaj osób zatwierdzających można ustawić hasła użytkownika dla tej aplikacji?** Przełącz, aby **tak**.</span><span class="sxs-lookup"><span data-stu-id="b386b-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="b386b-171">**Opcjonalnie:** do określenia osób zatwierdzających biznesowych, którzy mogą zatwierdzić dostęp do tej aplikacji, kliknij przycisk wyboru obok etykiety **kto może zatwierdzić dostęp do tej aplikacji?** wybrać maksymalnie 10 firm poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="b386b-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="b386b-172">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b386b-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="b386b-173">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz przypisać do roli użytkowników samoobsługi zatwierdzone, kliknij selektor **do roli należy użytkowników można przypisać w tej aplikacji?** wybierz rolę, do której można przypisać tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b386b-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="b386b-174">Kliknij przycisk **zapisać** na górze bloku, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="b386b-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="b386b-175">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić do ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk **+ Dodaj** przycisk, aby znaleźć aplikacji, dla których włączono samoobsługi dostępu.</span><span class="sxs-lookup"><span data-stu-id="b386b-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="b386b-176">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="b386b-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="b386b-177">Można włączyć wiadomość e-mail z informacją, gdy użytkownik żąda dostępu do aplikacji, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="b386b-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="b386b-178">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że jeśli określisz wiele osób zatwierdzających żadnych jedna osoba zatwierdzająca może osoba zatwierdzająca dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b386b-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b386b-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b386b-179">Next steps</span></span>
[<span data-ttu-id="b386b-180">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="b386b-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
