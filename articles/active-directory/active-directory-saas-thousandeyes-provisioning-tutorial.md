---
title: "Samouczek: Konfigurowanie ThousandEyes dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooThousandEyes tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="26465-103">Samouczek: Konfigurowanie ThousandEyes dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="26465-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="26465-104">Celem Hello tego samouczka jest tooshow hello kroki potrzebne tooperform rezerw tooautomatically ThousandEyes i Azure AD i anulować aprowizację kont użytkowników z usługi Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="26465-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="26465-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26465-105">Prerequisites</span></span>

<span data-ttu-id="26465-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="26465-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="26465-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="26465-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="26465-108">Dzierżawcy ThousandEyes z hello [planu Standard](https://www.thousandeyes.com/pricing) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="26465-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="26465-109">Konto użytkownika z uprawnieniami administratora w ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="26465-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="26465-110">Hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), które jest dostępne tooThousandEyes zespoły w planie Standard hello lub większą.</span><span class="sxs-lookup"><span data-stu-id="26465-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="26465-111">Przypisywanie użytkowników tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="26465-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="26465-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="26465-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="26465-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="26465-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="26465-114">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji ThousandEyes tooyour.</span><span class="sxs-lookup"><span data-stu-id="26465-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="26465-115">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour ThousandEyes aplikacji:</span><span class="sxs-lookup"><span data-stu-id="26465-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="26465-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="26465-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="26465-117">Ważne porady dotyczące przypisywania tooThousandEyes użytkowników</span><span class="sxs-lookup"><span data-stu-id="26465-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="26465-118">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooThousandEyes inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="26465-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="26465-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="26465-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="26465-120">Podczas przypisywania tooThousandEyes użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="26465-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="26465-121">Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="26465-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="26465-122">Konfigurowanie inicjowania obsługi administracyjnej tooThousandEyes użytkownika</span><span class="sxs-lookup"><span data-stu-id="26465-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="26465-123">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooThousandEyes programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w ThousandEyes w oparciu o przypisania użytkowników i grup w Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26465-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="26465-124">Można też tooenabled na języku SAML logowania jednokrotnego dla ThousandEyes hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26465-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="26465-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="26465-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="26465-126">Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooThousandEyes w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="26465-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="26465-127">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="26465-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="26465-128">ThousandEyes został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem ThousandEyes za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="26465-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="26465-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **ThousandEyes** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="26465-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="26465-130">Wybierz ThousandEyes z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26465-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="26465-131">Wybierz wystąpienia programu ThousandEyes, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="26465-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="26465-132">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="26465-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![ThousandEyes inicjowania obsługi administracyjnej](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="26465-134">W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **klucz tajny tokenu** generowane przez konto użytkownika ThousandEyes (hello token znajduje się na koncie ThousandEyes: **zabezpieczeń & Uwierzytelnianie**).</span><span class="sxs-lookup"><span data-stu-id="26465-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes inicjowania obsługi administracyjnej](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="26465-136">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour ThousandEyes aplikację.</span><span class="sxs-lookup"><span data-stu-id="26465-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="26465-137">Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto ThousandEyes ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="26465-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="26465-138">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."</span><span class="sxs-lookup"><span data-stu-id="26465-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="26465-139">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="26465-139">Click **Save**.</span></span> 

9. <span data-ttu-id="26465-140">W obszarze hello sekcji mapowania, wybierz **tooThousandEyes synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="26465-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="26465-141">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="26465-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="26465-142">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom ThousandEyes dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="26465-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="26465-143">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="26465-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="26465-144">tooenable hello inicjowania obsługi usługi Azure AD dla ThousandEyes, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="26465-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="26465-145">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="26465-145">Click **Save**.</span></span> 

<span data-ttu-id="26465-146">Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooThousandEyes w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="26465-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="26465-147">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="26465-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="26465-148">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="26465-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="26465-149">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="26465-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="26465-150">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="26465-150">Additional resources</span></span>

* [<span data-ttu-id="26465-151">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="26465-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="26465-152">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26465-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="26465-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26465-153">Next steps</span></span>

* [<span data-ttu-id="26465-154">Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="26465-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
