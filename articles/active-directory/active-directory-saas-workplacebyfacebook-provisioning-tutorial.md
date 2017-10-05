---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="b402c-103">Samouczek: Konfigurowanie miejsca pracy przez usługi Facebook na potrzeby Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="b402c-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="b402c-104">Celem tego samouczka jest opisano czynności, które należy wykonać w miejscu pracy przez Facebook i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b402c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b402c-105">Prerequisites</span></span>

<span data-ttu-id="b402c-106">Aby skonfigurować integrację usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b402c-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="b402c-107">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b402c-107">An Azure AD subscription</span></span>
- <span data-ttu-id="b402c-108">Pracy przez Facebook jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b402c-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b402c-109">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b402c-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b402c-110">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b402c-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b402c-111">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b402c-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b402c-112">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b402c-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="b402c-113">Przypisywanie użytkowników do miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="b402c-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="b402c-114">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b402c-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b402c-115">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="b402c-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b402c-116">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="b402c-117">Po decyzję, można przypisać użytkowników do miejsca pracy przez aplikację usługi Facebook postępując zgodnie z instrukcjami w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="b402c-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="b402c-118">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="b402c-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="b402c-119">Ważne porady dotyczące przypisywania użytkowników do miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="b402c-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="b402c-120">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany do miejsca pracy przez Facebook do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b402c-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="b402c-121">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="b402c-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b402c-122">Przypisanie użytkownika do miejsca pracy przez usługi Facebook, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b402c-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="b402c-123">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b402c-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="b402c-124">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="b402c-124">Enable User Provisioning</span></span>

<span data-ttu-id="b402c-125">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD do miejsca pracy przez konto użytkownika usługi Facebook na inicjowanie obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w pracy przez usługi Facebook na podstawie przypisań użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b402c-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b402c-126">Można też włączyć na języku SAML logowania jednokrotnego dla miejsca pracy przez usługi Facebook, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b402c-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b402c-127">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="b402c-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="b402c-128">Aby skonfigurować użytkownika Inicjowanie obsługi konta w serwisie Facebook w miejscu pracy w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b402c-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="b402c-129">Celem tej sekcji jest przedstawiają sposób włączania obsługi kont użytkowników usługi Active Directory do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="b402c-130">Usługi Azure AD umożliwia automatyczną synchronizację szczegóły konta użytkowników przypisane do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="b402c-131">To automatyczną synchronizację umożliwia dołączanie przez Facebook, aby pobrać dane, należy go autoryzacji użytkowników dostępu przed ich próbował zarejestrować się po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="b402c-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="b402c-132">Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b402c-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="b402c-133">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b402c-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="b402c-134">Obszar roboczy w serwisie Facebook został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia miejsca pracy przez usługi Facebook, korzystając z pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b402c-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="b402c-135">W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b402c-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="b402c-136">Wybierz obszar roboczy w serwisie Facebook w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b402c-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b402c-137">Wybierz wystąpienia programu miejsca pracy przez usługi Facebook, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="b402c-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b402c-138">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="b402c-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b402c-140">W obszarze **poświadczeń administratora** wprowadź klucz tajny tokenu i adres URL dzierżawy z miejsca pracy przez administratora usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="b402c-141">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="b402c-142">Jeśli połączenie nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="b402c-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="b402c-143">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="b402c-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="b402c-144">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="b402c-144">Click **Save.**</span></span>

9. <span data-ttu-id="b402c-145">W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do miejsca pracy przez usługi Facebook.**</span><span class="sxs-lookup"><span data-stu-id="b402c-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="b402c-146">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="b402c-147">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w miejscu pracy przez Facebook dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="b402c-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="b402c-148">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="b402c-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="b402c-149">Aby włączyć usługi Azure AD, świadczenie usługi dla miejsca pracy przez usługi Facebook, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="b402c-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="b402c-150">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="b402c-150">Click **Save.**</span></span>

<span data-ttu-id="b402c-151">Aby uzyskać więcej informacji na temat konfigurowania automatycznego inicjowania obsługi administracyjnej, zobacz [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="b402c-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="b402c-152">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="b402c-152">You can now create a test account.</span></span> <span data-ttu-id="b402c-153">Poczekaj maksymalnie 20 minut, aby sprawdzić, czy konto zostało zsynchronizowane w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b402c-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b402c-154">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b402c-154">Additional resources</span></span>

* [<span data-ttu-id="b402c-155">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="b402c-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b402c-156">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b402c-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b402c-157">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b402c-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

