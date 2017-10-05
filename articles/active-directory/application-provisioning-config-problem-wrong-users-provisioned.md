---
title: "Nieprawidłowy zestaw użytkowników są aprowizowany do aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dowiedzieć się, dlaczego inny zestaw użytkowników są aprowizowany do aplikacji niż te, które miały"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="9b0f9-103">Nieprawidłowy zestaw użytkowników są aprowizowany do aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b0f9-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="9b0f9-104">Użytkowników, którzy są udostępnione do aplikacji głównie wynikają z których użytkownicy i grupy zostały **przypisane** do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="9b0f9-105">Użyj zasoby przedstawione poniżej, aby dowiedzieć się, jak sprawdzić, którzy użytkownicy i grupy z przypisanym do aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="9b0f9-106">Przypisywanie użytkownika bezpośrednio jako administrator</span><span class="sxs-lookup"><span data-stu-id="9b0f9-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="9b0f9-107">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b0f9-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9b0f9-108">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="9b0f9-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9b0f9-109">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b0f9-110">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b0f9-111">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b0f9-112">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9b0f9-113">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9b0f9-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b0f9-114">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9b0f9-115">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b0f9-116">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9b0f9-117">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9b0f9-118">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9b0f9-119">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9b0f9-120">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9b0f9-121">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9b0f9-122">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9b0f9-123">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9b0f9-124">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9b0f9-125">Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy powinna być przygotowana do aplikacji w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="9b0f9-126">Sprawdź **dzienników inspekcji** szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="9b0f9-127">Przypisz grupę bezpośrednio do aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="9b0f9-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="9b0f9-128">Aby przypisać co najmniej jedną grupę aplikacji bezpośrednio, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b0f9-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9b0f9-129">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="9b0f9-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9b0f9-130">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b0f9-131">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b0f9-132">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b0f9-133">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9b0f9-134">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="9b0f9-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b0f9-135">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9b0f9-136">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b0f9-137">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9b0f9-138">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9b0f9-139">Wpisz w **grupy Pełna nazwa** planuje się przypisanie do grupy **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9b0f9-140">Umieść kursor nad **grupy** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9b0f9-141">Kliknij pole wyboru obok profilu zdjęcie lub logo, aby dodać użytkownika do grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9b0f9-142">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jedną grupę**, typu w innym **grupy Pełna nazwa** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać tę grupę do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="9b0f9-143">Po wybraniu grup kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9b0f9-144">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="9b0f9-145">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="9b0f9-146">Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy, zawarte w obrębie grupy powinna być przygotowana do aplikacji w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="9b0f9-147">Sprawdź **dzienników inspekcji** szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9b0f9-148">Inicjowanie obsługi administracyjnej Nazwa grupy i szczegóły grupy, oprócz członków, jeśli są obsługiwane w przypadku niektórych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="9b0f9-149">Można włączyć lub wyłączyć tę funkcję przez włączenie lub wyłączenie **mapowania** dla obiektów grupy pokazano **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="9b0f9-150">Jeśli Inicjowanie obsługi grup jest włączone, należy przejrzeć mapowań atrybutów do upewnij się, że odpowiednie pole jest używany przez "Pasujących ID".</span><span class="sxs-lookup"><span data-stu-id="9b0f9-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="9b0f9-151">Może to być nazwa wyświetlana lub e-mail aliasu, jak grupy i jej elementów członkowskich nie można zainicjować obsługi administracyjnej Jeśli zgodnej właściwości jest pusta lub nie wypełnione grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b0f9-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b0f9-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b0f9-152">Next steps</span></span>
[<span data-ttu-id="9b0f9-153">Automatyzowanie użytkownika alokowania i anulowania alokowania do aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b0f9-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
