---
title: 'Samouczek: Integracji Azure Active Directory z Jive | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="03adf-103">Samouczek: Konfigurowanie Jive Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="03adf-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="03adf-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Jive i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="03adf-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03adf-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="03adf-105">Prerequisites</span></span>

<span data-ttu-id="03adf-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="03adf-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="03adf-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="03adf-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="03adf-108">Jive jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="03adf-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="03adf-109">Konto użytkownika w Jive z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="03adf-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="03adf-110">Przypisywanie użytkowników tooJive</span><span class="sxs-lookup"><span data-stu-id="03adf-110">Assigning users tooJive</span></span>

<span data-ttu-id="03adf-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="03adf-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="03adf-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="03adf-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="03adf-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour Jive aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03adf-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="03adf-114">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Jive aplikacji:</span><span class="sxs-lookup"><span data-stu-id="03adf-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="03adf-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="03adf-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="03adf-116">Ważne porady dotyczące przypisywania tooJive użytkowników</span><span class="sxs-lookup"><span data-stu-id="03adf-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="03adf-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooJive inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="03adf-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="03adf-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="03adf-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="03adf-119">Podczas przypisywania tooJive użytkownika, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03adf-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="03adf-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="03adf-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="03adf-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="03adf-121">Enable User Provisioning</span></span>

<span data-ttu-id="03adf-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooJive programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Jive w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03adf-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="03adf-123">Można też tooenabled na języku SAML rejestracji jednokrotnej dla Jive hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03adf-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03adf-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="03adf-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="03adf-125">Przypisywanie konta użytkowników tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="03adf-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="03adf-126">Celem Hello w tej sekcji jest toooutline jak tooJive kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="03adf-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="03adf-127">W ramach tej procedury jest wymagana tooprovide należy toorequest z Jive.com token zabezpieczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03adf-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="03adf-128">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="03adf-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="03adf-129">Jive został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Jive za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="03adf-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="03adf-130">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Jive** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="03adf-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="03adf-131">Wybierz Jive z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03adf-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="03adf-132">Wybierz wystąpienia programu Jive, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="03adf-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="03adf-133">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="03adf-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="03adf-135">W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="03adf-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="03adf-136">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-136">a.</span></span> <span data-ttu-id="03adf-137">W hello **nazwa użytkownika administratora Jive** tekstowym, wpisz nazwę, która ma hello konta Jive **administratorem** profil Jive.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="03adf-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="03adf-138">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-138">b.</span></span> <span data-ttu-id="03adf-139">W hello **hasło administratora Jive** tekstowym, wpisz hello hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="03adf-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="03adf-140">c.</span><span class="sxs-lookup"><span data-stu-id="03adf-140">c.</span></span> <span data-ttu-id="03adf-141">W hello **adres URL dzierżawy Jive** pole tekstowe, typ hello Jive — adres URL dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="03adf-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="03adf-142">adres URL dzierżawy Jive Hello jest adres URL, który jest używany przez toolog Twojej organizacji w tooJive.</span><span class="sxs-lookup"><span data-stu-id="03adf-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="03adf-143">Zwykle adres URL hello ma hello następującego formatu: **www.\< Organizacja\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="03adf-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="03adf-144">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Jive aplikację.</span><span class="sxs-lookup"><span data-stu-id="03adf-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="03adf-145">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="03adf-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="03adf-146">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="03adf-146">Click **Save.**</span></span>

9. <span data-ttu-id="03adf-147">W obszarze hello sekcji mapowania, wybierz **tooJive synchronizacji Azure Active Directory użytkowników.**</span><span class="sxs-lookup"><span data-stu-id="03adf-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="03adf-148">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="03adf-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="03adf-149">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Jive dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="03adf-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="03adf-150">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="03adf-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="03adf-151">tooenable hello inicjowania obsługi usługi Azure AD dla Jive, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="03adf-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="03adf-152">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="03adf-152">Click **Save.**</span></span>

<span data-ttu-id="03adf-153">Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooJive w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="03adf-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="03adf-154">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="03adf-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="03adf-155">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello usługi w aplikacji Jive inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="03adf-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="03adf-156">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="03adf-156">You can now create a test account.</span></span> <span data-ttu-id="03adf-157">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooJive.</span><span class="sxs-lookup"><span data-stu-id="03adf-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03adf-158">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="03adf-158">Additional resources</span></span>

* [<span data-ttu-id="03adf-159">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="03adf-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03adf-160">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03adf-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="03adf-161">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="03adf-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)