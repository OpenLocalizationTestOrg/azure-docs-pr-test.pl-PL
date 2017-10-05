---
title: "Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do miejsca pracy przez usługi Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: a347eedbf5511dc83e1bc7721667441cfb87cb59
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="9594d-103">Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="9594d-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="9594d-104">W tym samouczku przedstawiono kroki niezbędne do automatycznego udostępniania i usuwanie kont użytkowników z usługi Azure Active Directory (Azure AD) do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-104">This tutorial shows you the steps necessary to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9594d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9594d-105">Prerequisites</span></span>

<span data-ttu-id="9594d-106">Aby skonfigurować integrację usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9594d-106">To configure Azure AD integration with Workplace by Facebook, you need the following:</span></span>

- <span data-ttu-id="9594d-107">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9594d-107">An Azure AD subscription</span></span>
- <span data-ttu-id="9594d-108">Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9594d-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9594d-109">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9594d-109">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9594d-110">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9594d-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9594d-111">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9594d-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-workplace-by-facebook"></a><span data-ttu-id="9594d-112">Przypisywanie użytkowników do miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="9594d-112">Assign users to Workplace by Facebook</span></span>

<span data-ttu-id="9594d-113">Usługi Azure AD używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9594d-113">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9594d-114">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które zostały przypisane do aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="9594d-114">In the context of automatic user account provisioning, only the users and groups that have been assigned to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9594d-115">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, zdecyduj, jakie użytkowników i grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-115">Before configuring and enabling the provisioning service, decide what users and groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="9594d-116">Następnie można przypisać użytkowników do miejsca pracy przez aplikację usługi Facebook zgodnie z instrukcjami w [przypisać użytkownika lub grupy do aplikacji przedsiębiorstwa](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9594d-116">You can then assign these users to your Workplace by Facebook app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="9594d-117">Przetestuj konfigurację inicjowania obsługi administracyjnej, przypisując pojedynczego użytkownika usługi Azure AD do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-117">Test the provisioning configuration by assigning a single Azure AD user to Workplace by Facebook.</span></span> <span data-ttu-id="9594d-118">Przypisz później dodatkowych użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="9594d-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="9594d-119">Gdy użytkownik jest przypisany do miejsca pracy przez usługi Facebook, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9594d-119">When you assign a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="9594d-120">Rola domyślnego dostępu nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="9594d-120">The Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9594d-121">Włącz inicjowanie obsługi użytkowników automatycznych</span><span class="sxs-lookup"><span data-stu-id="9594d-121">Enable automated user provisioning</span></span>

<span data-ttu-id="9594d-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika, inicjowanie obsługi interfejsu API z miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-122">This section guides you through connecting your Azure AD to the user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="9594d-123">Możesz również Dowiedz się, jak skonfigurować usługę inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączenie konta użytkowników przypisane w pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-123">You also learn how to configure the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="9594d-124">To jest ustalane na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9594d-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9594d-125">Można również włączyć na języku SAML logowania jednokrotnego dla miejsca pracy przez Facebook, przez zgodnie z instrukcjami podanymi w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9594d-125">You can also choose to enabled SAML-based SSO for Workplace by Facebook, by following the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9594d-126">Chociaż te dwie funkcje uzupełniają logowania jednokrotnego można skonfigurować niezależnie od automatyczne udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="9594d-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="9594d-127">Skonfiguruj konto użytkownika do miejsca pracy przez Facebook inicjowania obsługi administracyjnej w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="9594d-127">Configure user account provisioning to Workplace by Facebook in Azure AD</span></span>

<span data-ttu-id="9594d-128">Usługi Azure AD umożliwia automatyczną synchronizację szczegóły konta użytkowników przypisane do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-128">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="9594d-129">To automatyczną synchronizację umożliwia dołączanie przez Facebook, aby pobrać dane, należy go autoryzacji użytkowników dostępu przed ich próbował zarejestrować się po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="9594d-129">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="9594d-130">Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9594d-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="9594d-131">W [portalu Azure](https://portal.azure.com), wybierz pozycję **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9594d-131">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="9594d-132">Jeśli skonfigurowano już miejsca pracy przez Facebook dla logowania jednokrotnego, wyszukiwanie wystąpienia miejsca pracy przez Facebook przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9594d-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using the search field.</span></span> <span data-ttu-id="9594d-133">W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9594d-133">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="9594d-134">Wybierz **miejsca pracy przez Facebook** w wynikach wyszukiwania i dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9594d-134">Select **Workplace by Facebook** from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9594d-135">Wybierz wystąpienie miejsca pracy przez usługi Facebook, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="9594d-135">Select your instance of Workplace by Facebook, and then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9594d-136">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="9594d-136">Set **Provisioning Mode** to **Automatic**.</span></span> 

    ![Zrzut ekranu z miejsca pracy przez opcje inicjowania obsługi usługi Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9594d-138">W obszarze **poświadczeń administratora** wprowadź **klucz tajny tokenu** i **adres URL dzierżawy** z miejsca pracy przez administratora usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-138">Under the **Admin Credentials** section, enter the **Secret Token** and the **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="9594d-139">W portalu Azure wybierz **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-139">In the Azure portal, select **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="9594d-140">Jeśli połączenie nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="9594d-140">If the connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="9594d-141">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="9594d-141">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the check box.</span></span>

8. <span data-ttu-id="9594d-142">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9594d-142">Select **Save**.</span></span>

9. <span data-ttu-id="9594d-143">W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="9594d-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.</span></span>

10. <span data-ttu-id="9594d-144">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="9594d-145">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w miejscu pracy przez Facebook dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="9594d-145">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="9594d-146">Aby zatwierdzić zmiany, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9594d-146">To commit any changes, select **Save**.</span></span>

11. <span data-ttu-id="9594d-147">Aby włączyć usługi Azure AD usługi dla miejsca pracy przez Facebook, inicjowania obsługi administracyjnej w **ustawienia** Zmień **stan inicjowania obsługi administracyjnej** do **na**.</span><span class="sxs-lookup"><span data-stu-id="9594d-147">To enable the Azure AD provisioning service for Workplace by Facebook, in the **Settings** section, change the **Provisioning Status** to **On**.</span></span>

12. <span data-ttu-id="9594d-148">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9594d-148">Select **Save**.</span></span>

<span data-ttu-id="9594d-149">Aby uzyskać więcej informacji na temat konfigurowania automatycznego inicjowania obsługi administracyjnej, zobacz [dokumentacji Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="9594d-149">For more information on how to configure automatic provisioning, see [the Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="9594d-150">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="9594d-150">You can now create a test account.</span></span> <span data-ttu-id="9594d-151">Poczekaj maksymalnie 20 minut, aby sprawdzić, czy konto zostało zsynchronizowane w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9594d-151">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9594d-152">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9594d-152">Additional resources</span></span>

* [<span data-ttu-id="9594d-153">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="9594d-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9594d-154">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9594d-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9594d-155">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9594d-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

