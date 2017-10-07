---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
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
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="325a2-103">Samouczek: Konfigurowanie miejsca pracy przez usługi Facebook na potrzeby Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="325a2-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="325a2-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w miejscu pracy przez Facebook i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="325a2-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="325a2-105">Prerequisites</span></span>

<span data-ttu-id="325a2-106">tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="325a2-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="325a2-107">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="325a2-107">An Azure AD subscription</span></span>
- <span data-ttu-id="325a2-108">Pracy przez Facebook jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="325a2-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="325a2-109">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="325a2-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="325a2-110">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="325a2-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="325a2-111">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="325a2-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="325a2-112">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="325a2-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="325a2-113">Przypisywanie użytkowników tooWorkplace przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="325a2-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="325a2-114">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="325a2-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="325a2-115">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="325a2-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="325a2-116">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="325a2-117">Po decyzję, można przypisać tych użytkowników tooyour miejsca pracy przez aplikację usługi Facebook, wykonując instrukcje hello tutaj:</span><span class="sxs-lookup"><span data-stu-id="325a2-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="325a2-118">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="325a2-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="325a2-119">Ważne porady dotyczące przypisywania tooWorkplace użytkowników przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="325a2-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="325a2-120">Zalecane jest pojedynczego użytkownika usługi Azure AD jest przypisywany tooWorkplace przez hello tootest Facebook inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="325a2-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="325a2-121">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="325a2-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="325a2-122">Podczas przypisywania tooWorkplace użytkownika przez usługi Facebook, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="325a2-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="325a2-123">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="325a2-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="325a2-124">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="325a2-124">Enable User Provisioning</span></span>

<span data-ttu-id="325a2-125">Ta sekcja przeprowadzi Cię przez łączenie z tooWorkplace usługi Azure AD przez konto użytkownika usługi Facebook na inicjowanie obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w pracy przez usługi Facebook na podstawie użytkownika i grupy przypisania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="325a2-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="325a2-126">Można też tooenabled na języku SAML logowania jednokrotnego dla miejsca pracy przez Facebook, po hello instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="325a2-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="325a2-127">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="325a2-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="325a2-128">konto użytkownika tooconfigure udostępniania tooWorkplace w serwisie Facebook w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="325a2-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="325a2-129">Celem Hello w tej sekcji jest toooutline jak tooenable użytkownika usługi Active Directory Inicjowanie obsługi administracyjnej kont tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="325a2-130">Azure obsługuje AD tooautomatically możliwości hello zsynchronizować hello szczegóły konta przypisane tooWorkplace użytkowników przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="325a2-131">To automatyczną synchronizację umożliwia dołączanie przez dane hello tooget Facebook tooauthorize użytkowników, aby uzyskać dostęp, wymaga przed ich próby toosign w przypadku powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="325a2-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="325a2-132">Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="325a2-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="325a2-133">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="325a2-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="325a2-134">Jeśli skonfigurowano już miejsca pracy przez Facebook dla logowania jednokrotnego, wyszukiwania dla swojego wystąpienia w miejscu pracy przez usługi Facebook za pomocą pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="325a2-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="325a2-135">W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="325a2-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="325a2-136">Wybierz obszar roboczy w serwisie Facebook z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="325a2-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="325a2-137">Wybierz wystąpienia programu miejsca pracy przez usługi Facebook, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="325a2-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="325a2-138">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="325a2-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="325a2-140">W obszarze hello **poświadczeń administratora** sekcji i wprowadź klucz tajny tokenu hello hello adres URL dzierżawy z miejsca pracy przez administratora usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="325a2-141">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour miejsca pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="325a2-142">Jeśli hello połączenia nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="325a2-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="325a2-143">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="325a2-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="325a2-144">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="325a2-144">Click **Save.**</span></span>

9. <span data-ttu-id="325a2-145">W obszarze hello sekcji mapowania, wybierz **tooWorkplace synchronizacji Azure Active Directory użytkowników przez usługi Facebook.**</span><span class="sxs-lookup"><span data-stu-id="325a2-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="325a2-146">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="325a2-147">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch kont użytkowników hello w miejscu pracy przez Facebook dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="325a2-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="325a2-148">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="325a2-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="325a2-149">tooenable hello inicjowania obsługi usługi Azure AD dla miejsca pracy przez Facebook, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="325a2-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="325a2-150">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="325a2-150">Click **Save.**</span></span>

<span data-ttu-id="325a2-151">Aby uzyskać więcej informacji na temat tooconfigure automatycznego inicjowania obsługi administracyjnej, zobacz [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="325a2-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="325a2-152">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="325a2-152">You can now create a test account.</span></span> <span data-ttu-id="325a2-153">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="325a2-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="325a2-154">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="325a2-154">Additional resources</span></span>

* [<span data-ttu-id="325a2-155">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="325a2-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="325a2-156">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="325a2-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="325a2-157">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="325a2-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

