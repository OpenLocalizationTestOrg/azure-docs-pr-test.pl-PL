---
title: "Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooautomatically udostępniania i usuwanie użytkowników z usługi Azure AD tooWorkplace przez usługi Facebook."
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
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="7508f-103">Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="7508f-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="7508f-104">Ten samouczek przedstawia hello tooautomatically niezbędne kroki zapewnianie i usuwanie kont użytkowników z usługi Azure Active Directory (Azure AD) tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7508f-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7508f-105">Prerequisites</span></span>

<span data-ttu-id="7508f-106">tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7508f-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="7508f-107">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7508f-107">An Azure AD subscription</span></span>
- <span data-ttu-id="7508f-108">Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7508f-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="7508f-109">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7508f-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="7508f-110">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7508f-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7508f-111">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7508f-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="7508f-112">Przypisywanie użytkowników tooWorkplace przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="7508f-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="7508f-113">Pojęcie o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu korzysta z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7508f-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="7508f-114">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały przypisane tooan aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="7508f-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="7508f-115">Aby zdecydować, skonfiguruj i Włącz hello inicjowania obsługi usługi, jakie użytkowników i grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="7508f-116">Następnie można przypisać te tooyour użytkowników miejsca pracy przez aplikację usługi Facebook, postępując hello instrukcjami [przypisanie użytkownika lub grupy aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7508f-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="7508f-117">Hello testu inicjowania obsługi konfiguracji przypisując pojedynczy tooWorkplace użytkownika usługi Azure AD przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="7508f-118">Przypisz później dodatkowych użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="7508f-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="7508f-119">Po przypisaniu tooWorkplace użytkownika przez usługi Facebook, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7508f-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="7508f-120">Hello roli domyślnego dostępu nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7508f-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="7508f-121">Włącz inicjowanie obsługi użytkowników automatycznych</span><span class="sxs-lookup"><span data-stu-id="7508f-121">Enable automated user provisioning</span></span>

<span data-ttu-id="7508f-122">Ta sekcja przeprowadzi Cię przez łączenie konta użytkownika usługi Azure AD toohello inicjowania obsługi interfejsu API z miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="7508f-123">Dowiesz się również, jak tooconfigure hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="7508f-124">To jest ustalane na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7508f-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="7508f-125">Możesz również tooenabled na języku SAML logowania jednokrotnego dla miejsca pracy przez Facebook, przez następujące hello instrukcjami hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7508f-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7508f-126">Chociaż te dwie funkcje uzupełniają logowania jednokrotnego można skonfigurować niezależnie od automatyczne udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="7508f-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="7508f-127">Skonfiguruj konto użytkownika w usłudze Azure AD inicjowania obsługi tooWorkplace przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="7508f-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="7508f-128">Azure obsługuje AD tooautomatically możliwości hello zsynchronizować hello szczegóły konta przypisane tooWorkplace użytkowników przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="7508f-129">To automatyczną synchronizację umożliwia dołączanie przez dane hello tooget Facebook tooauthorize użytkowników, aby uzyskać dostęp, wymaga przed ich próby toosign w przypadku powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="7508f-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="7508f-130">Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7508f-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="7508f-131">W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7508f-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="7508f-132">Jeśli skonfigurowano już miejsca pracy przez Facebook dla logowania jednokrotnego, wyszukiwania dla swojego wystąpienia w miejscu pracy przez usługi Facebook, przy użyciu hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7508f-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="7508f-133">W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7508f-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="7508f-134">Wybierz **miejsca pracy przez Facebook** z hello wyniki wyszukiwania i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7508f-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="7508f-135">Wybierz wystąpienia programu miejsca pracy przez usługi Facebook, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="7508f-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="7508f-136">Ustaw **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="7508f-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Zrzut ekranu z miejsca pracy przez opcje inicjowania obsługi usługi Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="7508f-138">W obszarze hello **poświadczeń administratora** wprowadź hello **klucz tajny tokenu** i hello **adres URL dzierżawy** z miejsca pracy przez administratora usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="7508f-139">Hello portalu Azure, wybierz **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="7508f-140">Witaj, połączenie nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="7508f-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="7508f-141">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="7508f-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="7508f-142">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7508f-142">Select **Save**.</span></span>

9. <span data-ttu-id="7508f-143">W obszarze hello sekcji mapowania, wybierz **tooWorkplace synchronizacji Azure Active Directory użytkowników przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="7508f-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="7508f-144">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="7508f-145">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch kont użytkowników hello w miejscu pracy przez Facebook dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="7508f-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="7508f-146">Wybierz wszystkie zmiany toocommit **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7508f-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="7508f-147">tooenable hello usługi inicjowania obsługi usługi Azure AD dla miejsca pracy przez Facebook, w hello **ustawienia** Zmień hello **stan inicjowania obsługi administracyjnej** za**na**.</span><span class="sxs-lookup"><span data-stu-id="7508f-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="7508f-148">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7508f-148">Select **Save**.</span></span>

<span data-ttu-id="7508f-149">Aby uzyskać więcej informacji na temat tooconfigure automatycznego inicjowania obsługi administracyjnej, zobacz [hello dokumentacji Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="7508f-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="7508f-150">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="7508f-150">You can now create a test account.</span></span> <span data-ttu-id="7508f-151">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="7508f-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7508f-152">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7508f-152">Additional resources</span></span>

* [<span data-ttu-id="7508f-153">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="7508f-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7508f-154">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7508f-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7508f-155">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7508f-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

