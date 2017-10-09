---
title: 'Samouczek: Integracji Azure Active Directory z Concur | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="80c62-103">Samouczek: Konfigurowanie cząstkowe do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="80c62-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="80c62-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Concur i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="80c62-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80c62-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80c62-105">Prerequisites</span></span>

<span data-ttu-id="80c62-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="80c62-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="80c62-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="80c62-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="80c62-108">Concur logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="80c62-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="80c62-109">Konto użytkownika w Concur z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="80c62-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="80c62-110">Przypisywanie użytkowników tooConcur</span><span class="sxs-lookup"><span data-stu-id="80c62-110">Assigning users tooConcur</span></span>

<span data-ttu-id="80c62-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="80c62-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="80c62-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="80c62-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="80c62-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Concur tooyour.</span><span class="sxs-lookup"><span data-stu-id="80c62-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="80c62-114">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Concur aplikacji:</span><span class="sxs-lookup"><span data-stu-id="80c62-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="80c62-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="80c62-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="80c62-116">Ważne porady dotyczące przypisywania tooConcur użytkowników</span><span class="sxs-lookup"><span data-stu-id="80c62-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="80c62-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooConcur inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="80c62-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="80c62-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="80c62-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="80c62-119">Podczas przypisywania tooConcur użytkownika, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80c62-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="80c62-120">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="80c62-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="80c62-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="80c62-121">Enable user provisioning</span></span>

<span data-ttu-id="80c62-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooConcur programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Concur w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c62-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="80c62-123">Można też tooenabled na języku SAML logowania jednokrotnego dla Concur hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80c62-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80c62-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="80c62-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="80c62-125">Przypisywanie konta użytkowników tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="80c62-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="80c62-126">Celem Hello w tej sekcji jest toooutline jak tooConcur kont tooenable Inicjowanie obsługi administracyjnej użytkownika usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80c62-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="80c62-127">aplikacje tooenable w hello usługi wydatków, ma prawidłową konfigurację toobe i korzystania z profilem administrator usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="80c62-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="80c62-128">Nie dodawaj hello WS Admin roli tooyour istniejący profil administratora używanej do T & j funkcji administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="80c62-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="80c62-129">Cząstkowe konsultantów lub powitania klienta administrator musi utworzyć różne profilu administratora usługi sieci Web i powitania klienta administrator musi używać tego profilu dla funkcji administratora usługi sieci Web hello (na przykład włączenie aplikacje).</span><span class="sxs-lookup"><span data-stu-id="80c62-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="80c62-130">Te profile muszą być przechowywane oddzielnie od powitania klienta administrator codzienne T & E admin profilu (hello T & E profilu administratora nie powinny mieć przypisanej roli WSAdmin hello).</span><span class="sxs-lookup"><span data-stu-id="80c62-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="80c62-131">Podczas tworzenia toobe profilu hello używane do włączania aplikacji hello nazwę administratora powitania klienta do pól profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="80c62-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="80c62-132">W ten sposób własność toohello profilu.</span><span class="sxs-lookup"><span data-stu-id="80c62-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="80c62-133">Po utworzeniu co najmniej jeden profil powitania klienta musi Zaloguj się za pomocą tego profilu hello tooclick "*włączyć*" przycisk aplikacji partnera w hello menu usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="80c62-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="80c62-134">Dla następujących powodów hello ta akcja nie można wykonać z profilem hello, używanego do normalnej T & E administracji.</span><span class="sxs-lookup"><span data-stu-id="80c62-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="80c62-135">Witaj klient ma toobe Witaj, który kliknie "*tak*" w oknie dialogu hello, w którym jest wyświetlany po włączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80c62-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="80c62-136">Kliknij ten przycisk uznaje się, że powitania klienta jest gotowi dla tooaccess aplikacji partnera hello ich danych, więc możesz lub hello partnera nie kliknij odpowiedni przycisk Tak.</span><span class="sxs-lookup"><span data-stu-id="80c62-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="80c62-137">Jeśli administrator klienta, która włączyła aplikację przy użyciu hello T & E profilu administratora pozostawia hello firmy (co w profilu hello jest dezaktywowane), wszystkie aplikacje włączone za pomocą tego profilu nie działa, aż do włączenia aplikacji hello z innym administratorem WS active profil.</span><span class="sxs-lookup"><span data-stu-id="80c62-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="80c62-138">Jest to, dlaczego powinni toocreate różne profile WS administratora.</span><span class="sxs-lookup"><span data-stu-id="80c62-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="80c62-139">Jeśli administrator pozostawia hello firmy, nazwę hello skojarzone toohello profilu WS administratora może być toohello zmienionych administratora zastąpienia, w razie potrzeby bez wpływu na powitania włączone, że aplikacji, ponieważ ten profil nie jest konieczne dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="80c62-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="80c62-140">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80c62-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="80c62-141">Zaloguj się na tooyour **Concur** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="80c62-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="80c62-142">Z hello **administracji** menu, wybierz opcję **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="80c62-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="80c62-143">![Dzierżawy Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur dzierżawy")</span><span class="sxs-lookup"><span data-stu-id="80c62-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="80c62-144">Na powitania po lewej stronie, z hello **usług sieci Web** okienku wybierz **Włącz aplikacji partnera**.</span><span class="sxs-lookup"><span data-stu-id="80c62-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="80c62-145">![Włączanie aplikacji partnera](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "włączyć partnera aplikacji")</span><span class="sxs-lookup"><span data-stu-id="80c62-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="80c62-146">Z hello **Włącz aplikacji** listy, wybierz **usługi Azure Active Directory**, a następnie kliknij przycisk **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="80c62-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="80c62-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="80c62-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="80c62-148">Kliknij przycisk **tak** tooclose hello **potwierdzenie akcji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80c62-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="80c62-149">![Potwierdzenie akcji](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "potwierdzenie akcji")</span><span class="sxs-lookup"><span data-stu-id="80c62-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="80c62-150">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="80c62-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="80c62-151">Concur został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Concur za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="80c62-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="80c62-152">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Concur** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="80c62-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="80c62-153">Wybierz Concur z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80c62-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="80c62-154">Wybierz wystąpienia programu Concur, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="80c62-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="80c62-155">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="80c62-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="80c62-157">W obszarze hello **poświadczeń administratora** wprowadź hello **nazwy użytkownika** i hello **hasło** administratora Concur.</span><span class="sxs-lookup"><span data-stu-id="80c62-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="80c62-158">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Concur aplikację.</span><span class="sxs-lookup"><span data-stu-id="80c62-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="80c62-159">Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto Concur ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="80c62-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="80c62-160">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="80c62-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="80c62-161">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="80c62-161">Click **Save.**</span></span>

14. <span data-ttu-id="80c62-162">W obszarze hello sekcji mapowania, wybierz **tooConcur synchronizacji Azure Active Directory użytkowników.**</span><span class="sxs-lookup"><span data-stu-id="80c62-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="80c62-163">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="80c62-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="80c62-164">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Concur dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="80c62-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="80c62-165">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="80c62-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="80c62-166">tooenable hello inicjowania obsługi usługi Azure AD dla Concur, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="80c62-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="80c62-167">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="80c62-167">Click **Save.**</span></span>

<span data-ttu-id="80c62-168">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="80c62-168">You can now create a test account.</span></span> <span data-ttu-id="80c62-169">Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooConcur.</span><span class="sxs-lookup"><span data-stu-id="80c62-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80c62-170">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="80c62-170">Additional resources</span></span>

* [<span data-ttu-id="80c62-171">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="80c62-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80c62-172">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80c62-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="80c62-173">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="80c62-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

