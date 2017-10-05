---
title: "Jak usunąć dostępu użytkownika do aplikacji | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu usuwania dostępu użytkownika do aplikacji"
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
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="73810-103">Jak usunąć dostępu użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="73810-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="73810-104">Ten artykuł ułatwia zrozumienie sposobu usuwania dostępu użytkownika do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73810-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="73810-105">Usunąć przypisanie określonego użytkownika lub grupy do aplikacji</span><span class="sxs-lookup"><span data-stu-id="73810-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="73810-106">Aby usunąć przypisanie grupy do aplikacji lub użytkownika, wykonaj czynności opisane w [Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="73810-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="73810-107">. ## chcę wyłączyć dostęp do aplikacji dla każdego użytkownika</span><span class="sxs-lookup"><span data-stu-id="73810-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="73810-108">Aby wyłączyć wszystkie logowania użytkownika do aplikacji, wykonaj czynności opisane w [wyłączyć logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artykułu.</span><span class="sxs-lookup"><span data-stu-id="73810-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="73810-109">Chcę, aby całkowicie usunąć aplikację</span><span class="sxs-lookup"><span data-stu-id="73810-109">I want to delete an application entirely</span></span>

<span data-ttu-id="73810-110">Aby **usunąć aplikację**, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="73810-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="73810-111">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="73810-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="73810-112">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="73810-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73810-113">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="73810-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73810-114">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73810-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="73810-115">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73810-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="73810-116">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="73810-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="73810-117">Wybierz aplikację, którą chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="73810-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="73810-118">Po załadowaniu aplikacji, kliknij przycisk **usunąć** ikony z najwyższym aplikacji **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="73810-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="73810-119">Chcę wyłączyć wszystkie operacje zgody przyszłych użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="73810-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="73810-120">Wyłączanie zgody użytkownika dla całego katalogu uniemożliwić użytkownikom końcowym zgodę dowolnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73810-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="73810-121">Administratorzy mogą nadal oznacza zgodę na behalves użytkownika.</span><span class="sxs-lookup"><span data-stu-id="73810-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="73810-122">Dowiedz się więcej o zgodę aplikacji i dlaczego może lub nie chcesz to zrobić, przeczytaj [zgody administratora i użytkownika opis](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="73810-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="73810-123">Aby **Wyłącz wszystkie operacje zgody użytkownika w przyszłości w katalogu cały**, postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="73810-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="73810-124">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="73810-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="73810-125">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="73810-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="73810-126">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="73810-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="73810-127">Kliknij przycisk **użytkowników i grup** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="73810-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="73810-128">Kliknij przycisk **ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="73810-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="73810-129">Wyłącz wszystkie operacje zgody użytkownika w przyszłości przez ustawienie **użytkownicy mogą zezwolić aplikacjom na dostęp do danych** Przełącz, aby **nr** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="73810-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="73810-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73810-130">Next steps</span></span>
[<span data-ttu-id="73810-131">Zarządzanie dostępem do aplikacji</span><span class="sxs-lookup"><span data-stu-id="73810-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
