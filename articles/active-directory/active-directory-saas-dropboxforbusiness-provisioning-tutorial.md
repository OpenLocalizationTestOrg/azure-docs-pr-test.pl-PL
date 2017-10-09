---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="8d025-103">Samouczek: Konfigurowanie skrzynki dla firm użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="8d025-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="8d025-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Dropbox dla firm i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooDropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="8d025-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d025-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8d025-105">Prerequisites</span></span>

<span data-ttu-id="8d025-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8d025-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8d025-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="8d025-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="8d025-108">Dropbox dla firm jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8d025-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="8d025-109">Konto użytkownika w Dropbox dla firm z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="8d025-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="8d025-110">Przypisywanie użytkowników tooDropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="8d025-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="8d025-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="8d025-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8d025-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="8d025-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="8d025-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="8d025-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8d025-114">Po decyzję, można przypisać te skrzynki tooyour użytkowników dla aplikacji biznesowych, wykonując instrukcje hello tutaj:</span><span class="sxs-lookup"><span data-stu-id="8d025-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="8d025-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="8d025-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="8d025-116">Ważne porady dotyczące przypisywania tooDropbox użytkowników dla firm</span><span class="sxs-lookup"><span data-stu-id="8d025-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="8d025-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany tooDropbox dla firm tootest hello inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8d025-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="8d025-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="8d025-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8d025-119">Podczas przypisywania tooDropbox użytkownika dla firm, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d025-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="8d025-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="8d025-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="8d025-121">Włącz automatyczne Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="8d025-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="8d025-122">Ta sekcja przeprowadzi Cię przez łączenie z tooDropbox usługi Azure AD dla konta użytkownika firmy inicjowania obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Dropbox dla firm, w oparciu o użytkowników i grup przypisania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d025-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="8d025-123">Można też tooenabled na języku SAML logowania jednokrotnego dla skrzynki dla firm, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d025-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8d025-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="8d025-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="8d025-125">tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:</span><span class="sxs-lookup"><span data-stu-id="8d025-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="8d025-126">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8d025-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="8d025-127">Jeśli skonfigurowano już program Dropbox dla firm dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi Dropbox dla firm przy użyciu pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="8d025-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="8d025-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Dropbox dla firm** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8d025-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="8d025-129">Wybierz Dropbox dla firm z wyników wyszukiwania hello i dodać tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d025-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="8d025-130">Wybierz wystąpienie usługi Dropbox dla firm, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="8d025-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="8d025-131">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="8d025-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="8d025-133">W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="8d025-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8d025-134">Dropbox dla okna dialogowego logowania biznesowych zostanie otwarty w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8d025-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="8d025-135">Na powitania **logowania toolink tooDropbox z usługą Azure AD** dialogowym logowania tooyour Dropbox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="8d025-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="8d025-136">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d025-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="8d025-137">Upewnij się, chcieliby tooyour zmiany toomake uprawnienia usługi Azure Active Directory toogive Dropbox dla firm dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="8d025-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="8d025-138">Kliknij przycisk **Zezwalaj**.</span><span class="sxs-lookup"><span data-stu-id="8d025-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="8d025-139">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d025-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="8d025-140">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="8d025-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8d025-141">W przypadku niepowodzenia połączenia hello zapewnić usłudze Dropbox konto firmowe, ma uprawnienia administratora zespołu i spróbuj hello **"Autoryzuj"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="8d025-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="8d025-142">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="8d025-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="8d025-143">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="8d025-143">Click **Save.**</span></span>

11. <span data-ttu-id="8d025-144">W obszarze hello sekcji mapowania, wybierz **tooDropbox synchronizacji Azure Active Directory użytkowników dla firm.**</span><span class="sxs-lookup"><span data-stu-id="8d025-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="8d025-145">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooDropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="8d025-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="8d025-146">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom skrzynki dla firm dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="8d025-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="8d025-147">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="8d025-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="8d025-148">tooenable hello inicjowania obsługi usługi Azure AD dla skrzynki dla firm, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="8d025-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="8d025-149">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="8d025-149">Click **Save.**</span></span>

<span data-ttu-id="8d025-150">Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooDropbox dla firm w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="8d025-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="8d025-151">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="8d025-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8d025-152">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="8d025-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="8d025-153">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="8d025-153">You can now create a test account.</span></span> <span data-ttu-id="8d025-154">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooDropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="8d025-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="8d025-155">Użytkownik pomyślnie zakończono inicjowanie obsługi cyklu wskazuje stan powiązane.</span><span class="sxs-lookup"><span data-stu-id="8d025-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="8d025-156">![Przypisywanie użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d025-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8d025-157">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8d025-157">Additional resources</span></span>

* [<span data-ttu-id="8d025-158">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8d025-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d025-159">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d025-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8d025-160">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8d025-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)