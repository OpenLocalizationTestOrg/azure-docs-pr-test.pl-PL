---
title: 'Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="16dee-103">Samouczek: Konfigurowanie Citrix GoToMeeting dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="16dee-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="16dee-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Citrix GoToMeeting i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="16dee-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16dee-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16dee-105">Prerequisites</span></span>

<span data-ttu-id="16dee-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="16dee-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="16dee-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="16dee-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="16dee-108">Citrix GoToMeeting jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="16dee-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="16dee-109">Konto użytkownika w Citrix GoToMeeting z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="16dee-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="16dee-110">Przypisywanie użytkowników tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="16dee-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="16dee-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="16dee-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="16dee-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="16dee-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="16dee-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą korzystać tooyour Citrix GoToMeeting aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16dee-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="16dee-114">Po decyzję, można przypisać tooyour tych użytkowników aplikacji Citrix GoToMeeting, wykonując instrukcje hello tutaj:</span><span class="sxs-lookup"><span data-stu-id="16dee-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="16dee-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="16dee-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="16dee-116">Ważne porady dotyczące przypisywania użytkowników tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="16dee-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="16dee-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest GoToMeeting tooCitrix inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16dee-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="16dee-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="16dee-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="16dee-119">Podczas przypisywania tooCitrix użytkownika GoToMeeting, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16dee-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="16dee-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="16dee-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="16dee-121">Włącz automatyczne Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="16dee-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="16dee-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika GoToMeeting tooCitrix usługi Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz przypisany użytkownik kont w Citrix GoToMeeting opartych na użytkowników i grup przypisania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16dee-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="16dee-123">Można też tooenabled na języku SAML logowania jednokrotnego dla Citrix GoToMeeting, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16dee-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16dee-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="16dee-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="16dee-125">tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:</span><span class="sxs-lookup"><span data-stu-id="16dee-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="16dee-126">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="16dee-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="16dee-127">Citrix GoToMeeting został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienie usługi przy użyciu pola wyszukiwania hello Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="16dee-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="16dee-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Citrix GoToMeeting** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="16dee-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="16dee-129">Wybierz Citrix GoToMeeting z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16dee-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="16dee-130">Wybierz wystąpienia programu Citrix GoToMeeting, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="16dee-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="16dee-131">Zestaw hello **inicjowania obsługi administracyjnej** tryb zbyt**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="16dee-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="16dee-133">W obszarze hello sekcji poświadczenia administratora wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="16dee-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="16dee-134">a.</span><span class="sxs-lookup"><span data-stu-id="16dee-134">a.</span></span> <span data-ttu-id="16dee-135">W hello **nazwa użytkownika administratora GoToMeeting Citrix** tekstowym, wpisz nazwę użytkownika hello administratora.</span><span class="sxs-lookup"><span data-stu-id="16dee-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="16dee-136">b.</span><span class="sxs-lookup"><span data-stu-id="16dee-136">b.</span></span> <span data-ttu-id="16dee-137">W hello **hasło administratora GoToMeeting Citrix** pole tekstowe, hasło administratora hello.</span><span class="sxs-lookup"><span data-stu-id="16dee-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="16dee-138">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour Citrix GoToMeeting aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16dee-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="16dee-139">Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto Citrix GoToMeeting ma uprawnienia administratora zespołu i spróbuj hello **"Poświadczeń administratora"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="16dee-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="16dee-140">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="16dee-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="16dee-141">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="16dee-141">Click **Save.**</span></span>

9. <span data-ttu-id="16dee-142">W obszarze hello sekcji mapowania, wybierz **tooCitrix synchronizacji Azure Active Directory użytkowników GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="16dee-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="16dee-143">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="16dee-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="16dee-144">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Citrix GoToMeeting dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="16dee-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="16dee-145">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="16dee-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="16dee-146">tooenable hello inicjowania obsługi usługi Azure AD dla Citrix GoToMeeting, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="16dee-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="16dee-147">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="16dee-147">Click **Save.**</span></span>

<span data-ttu-id="16dee-148">Rozpoczyna hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooCitrix GoToMeeting w sekcji hello użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="16dee-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="16dee-149">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="16dee-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="16dee-150">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="16dee-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16dee-151">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="16dee-151">Additional resources</span></span>

* [<span data-ttu-id="16dee-152">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="16dee-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16dee-153">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16dee-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="16dee-154">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="16dee-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


