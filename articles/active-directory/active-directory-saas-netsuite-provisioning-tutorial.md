---
title: 'Samouczek: Integracji Azure Active Directory z Netsuite | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="a1423-103">Samouczek: Konfigurowanie Netsuite dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a1423-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="a1423-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Netsuite i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="a1423-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1423-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a1423-105">Prerequisites</span></span>

<span data-ttu-id="a1423-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a1423-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="a1423-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="a1423-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a1423-108">Netsuite jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a1423-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="a1423-109">Konto użytkownika w Netsuite z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="a1423-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="a1423-110">Przypisywanie użytkowników tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="a1423-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="a1423-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="a1423-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="a1423-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="a1423-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="a1423-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Netsuite tooyour.</span><span class="sxs-lookup"><span data-stu-id="a1423-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="a1423-114">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Netsuite aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a1423-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="a1423-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="a1423-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="a1423-116">Ważne porady dotyczące przypisywania tooNetsuite użytkowników</span><span class="sxs-lookup"><span data-stu-id="a1423-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="a1423-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooNetsuite inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a1423-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="a1423-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="a1423-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a1423-119">Podczas przypisywania tooNetsuite użytkownika, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a1423-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="a1423-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a1423-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a1423-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a1423-121">Enable User Provisioning</span></span>

<span data-ttu-id="a1423-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooNetsuite programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Netsuite w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1423-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="a1423-123">Można też tooenabled na języku SAML logowania jednokrotnego dla Netsuite hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1423-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a1423-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="a1423-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="a1423-125">Przypisywanie konta użytkowników tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a1423-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="a1423-126">Celem Hello w tej sekcji jest toooutline jak tooNetsuite kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a1423-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="a1423-127">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1423-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a1423-128">Netsuite został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Netsuite za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a1423-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="a1423-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Netsuite** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a1423-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="a1423-130">Wybierz Netsuite z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a1423-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="a1423-131">Wybierz wystąpienia programu Netsuite, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="a1423-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="a1423-132">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="a1423-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a1423-134">W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a1423-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="a1423-135">a.</span><span class="sxs-lookup"><span data-stu-id="a1423-135">a.</span></span> <span data-ttu-id="a1423-136">W hello **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która ma hello konta Netsuite **administratorem** profil Netsuite.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="a1423-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="a1423-137">b.</span><span class="sxs-lookup"><span data-stu-id="a1423-137">b.</span></span> <span data-ttu-id="a1423-138">W hello **hasło administratora** tekstowym, wpisz hello hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="a1423-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="a1423-139">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Netsuite aplikację.</span><span class="sxs-lookup"><span data-stu-id="a1423-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="a1423-140">W hello **wiadomość E-mail z powiadomieniem** wprowadź hello adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="a1423-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="a1423-141">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a1423-141">Click **Save.**</span></span>

9. <span data-ttu-id="a1423-142">W obszarze hello sekcji mapowania, wybierz **tooNetsuite synchronizacji Azure Active Directory użytkowników.**</span><span class="sxs-lookup"><span data-stu-id="a1423-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="a1423-143">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="a1423-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="a1423-144">Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości są używane toomatch hello kontom Netsuite dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="a1423-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="a1423-145">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="a1423-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="a1423-146">tooenable hello inicjowania obsługi usługi Azure AD dla Netsuite, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="a1423-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="a1423-147">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a1423-147">Click **Save.**</span></span>

<span data-ttu-id="a1423-148">Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooNetsuite w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1423-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="a1423-149">Należy pamiętać, że tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello przyjmuje hello synchronizacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="a1423-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="a1423-150">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello usługi w aplikacji Netsuite inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a1423-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="a1423-151">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="a1423-151">You can now create a test account.</span></span> <span data-ttu-id="a1423-152">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="a1423-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1423-153">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a1423-153">Additional resources</span></span>

* [<span data-ttu-id="a1423-154">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="a1423-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1423-155">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1423-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a1423-156">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a1423-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)