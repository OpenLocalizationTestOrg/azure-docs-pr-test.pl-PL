---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="34d3d-103">Samouczek: Konfigurowanie DocuSign Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="34d3d-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="34d3d-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w DocuSign i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="34d3d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34d3d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34d3d-105">Prerequisites</span></span>

<span data-ttu-id="34d3d-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="34d3d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="34d3d-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="34d3d-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="34d3d-108">DocuSign logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34d3d-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="34d3d-109">Konto użytkownika w DocuSign z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="34d3d-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="34d3d-110">Przypisywanie użytkowników tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="34d3d-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="34d3d-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="34d3d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="34d3d-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="34d3d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="34d3d-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji DocuSign tooyour.</span><span class="sxs-lookup"><span data-stu-id="34d3d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="34d3d-114">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour DocuSign aplikacji:</span><span class="sxs-lookup"><span data-stu-id="34d3d-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="34d3d-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="34d3d-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="34d3d-116">Ważne porady dotyczące przypisywania tooDocuSign użytkowników</span><span class="sxs-lookup"><span data-stu-id="34d3d-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="34d3d-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooDocuSign inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34d3d-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="34d3d-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="34d3d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="34d3d-119">Podczas przypisywania tooDocuSign użytkownika, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="34d3d-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="34d3d-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="34d3d-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="34d3d-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="34d3d-121">Enable User Provisioning</span></span>

<span data-ttu-id="34d3d-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooDocuSign programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w DocuSign w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34d3d-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="34d3d-123">Można też tooenabled na języku SAML logowania jednokrotnego dla DocuSign hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34d3d-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="34d3d-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="34d3d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="34d3d-125">Przypisywanie konta użytkowników tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="34d3d-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="34d3d-126">Celem Hello w tej sekcji jest toooutline jak tooDocuSign kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="34d3d-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="34d3d-127">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="34d3d-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="34d3d-128">DocuSign został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem DocuSign za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34d3d-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="34d3d-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **DocuSign** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="34d3d-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="34d3d-130">Wybierz DocuSign z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34d3d-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="34d3d-131">Wybierz wystąpienia programu DocuSign, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="34d3d-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="34d3d-132">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="34d3d-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="34d3d-134">W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="34d3d-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="34d3d-135">a.</span><span class="sxs-lookup"><span data-stu-id="34d3d-135">a.</span></span> <span data-ttu-id="34d3d-136">W hello **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która ma hello konta DocuSign **administratorem** profil DocuSign.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="34d3d-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="34d3d-137">b.</span><span class="sxs-lookup"><span data-stu-id="34d3d-137">b.</span></span> <span data-ttu-id="34d3d-138">W hello **hasło administratora** tekstowym, wpisz hello hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="34d3d-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="34d3d-139">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour DocuSign aplikację.</span><span class="sxs-lookup"><span data-stu-id="34d3d-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="34d3d-140">W hello **wiadomość E-mail z powiadomieniem** wprowadź hello adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="34d3d-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="34d3d-141">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="34d3d-141">Click **Save.**</span></span>

9. <span data-ttu-id="34d3d-142">W obszarze hello sekcji mapowania, wybierz **tooDocuSign synchronizacji Azure Active Directory użytkowników.**</span><span class="sxs-lookup"><span data-stu-id="34d3d-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="34d3d-143">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="34d3d-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="34d3d-144">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom DocuSign dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="34d3d-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="34d3d-145">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="34d3d-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="34d3d-146">tooenable hello inicjowania obsługi usługi Azure AD dla DocuSign, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="34d3d-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="34d3d-147">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="34d3d-147">Click **Save.**</span></span>

<span data-ttu-id="34d3d-148">Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooDocuSign w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="34d3d-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="34d3d-149">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="34d3d-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="34d3d-150">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello usługi w aplikacji DocuSign inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="34d3d-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="34d3d-151">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="34d3d-151">You can now create a test account.</span></span> <span data-ttu-id="34d3d-152">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="34d3d-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34d3d-153">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="34d3d-153">Additional resources</span></span>

* [<span data-ttu-id="34d3d-154">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="34d3d-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34d3d-155">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34d3d-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="34d3d-156">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="34d3d-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)