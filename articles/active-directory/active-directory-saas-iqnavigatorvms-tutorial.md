---
title: 'Samouczek: Integracji Azure Active Directory z maszynami Wirtualnymi IQNavigator | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i IQNavigator maszyn wirtualnych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="84a78-103">Samouczek: Integracji Azure Active Directory z IQNavigator maszyny Wirtualne</span><span class="sxs-lookup"><span data-stu-id="84a78-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="84a78-104">Z tego samouczka, dowiesz się, jak toointegrate IQNavigator maszyn wirtualnych w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84a78-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84a78-105">Integracja z usługą Azure AD IQNavigator maszyn wirtualnych zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="84a78-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84a78-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooIQNavigator maszyny Wirtualne</span><span class="sxs-lookup"><span data-stu-id="84a78-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="84a78-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIQNavigator maszyn wirtualnych (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="84a78-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84a78-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="84a78-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84a78-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84a78-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84a78-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84a78-110">Prerequisites</span></span>

<span data-ttu-id="84a78-111">tooconfigure integracji z usługą Azure AD IQNavigator maszyn wirtualnych, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="84a78-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="84a78-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="84a78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84a78-113">Maszyny Wirtualne IQNavigator logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="84a78-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84a78-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="84a78-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84a78-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="84a78-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84a78-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="84a78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84a78-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84a78-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84a78-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="84a78-118">Scenario description</span></span>
<span data-ttu-id="84a78-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="84a78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84a78-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="84a78-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84a78-121">Dodawanie IQNavigator maszyn wirtualnych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="84a78-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="84a78-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="84a78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="84a78-123">Dodawanie IQNavigator maszyn wirtualnych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="84a78-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="84a78-124">tooconfigure hello integracji IQNavigator maszyn wirtualnych w usłudze Azure Active Directory, należy tooadd IQNavigator maszyn wirtualnych z galerii hello tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="84a78-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84a78-125">**tooadd maszyn wirtualnych IQNavigator z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="84a78-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84a78-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="84a78-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="84a78-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="84a78-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84a78-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="84a78-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="84a78-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="84a78-133">W polu wyszukiwania hello wpisz **maszyn wirtualnych IQNavigator**.</span><span class="sxs-lookup"><span data-stu-id="84a78-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="84a78-135">W panelu wyników hello, wybierz **IQNavigator maszyn wirtualnych**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="84a78-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84a78-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="84a78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84a78-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z maszynami Wirtualnymi IQNavigator w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84a78-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello na maszynach wirtualnych IQNavigator jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84a78-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="84a78-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi na maszynach wirtualnych IQNavigator musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="84a78-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="84a78-141">Na maszynach wirtualnych IQNavigator, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="84a78-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84a78-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej IQNavigator maszyn wirtualnych, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="84a78-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84a78-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="84a78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84a78-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="84a78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84a78-145">**[Tworzenie użytkownika testowego maszyn wirtualnych IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave odpowiednikiem Simona Britta na maszynach wirtualnych IQNavigator, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="84a78-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84a78-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="84a78-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84a78-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="84a78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84a78-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="84a78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84a78-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji IQNavigator maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84a78-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="84a78-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z maszynami Wirtualnymi IQNavigator, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="84a78-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="84a78-151">W portalu Azure na powitania hello **maszyn wirtualnych IQNavigator** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="84a78-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="84a78-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="84a78-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="84a78-155">Na powitania **IQNavigator domeny maszyn wirtualnych i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="84a78-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="84a78-157">a.</span><span class="sxs-lookup"><span data-stu-id="84a78-157">a.</span></span> <span data-ttu-id="84a78-158">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="84a78-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="84a78-159">b.</span><span class="sxs-lookup"><span data-stu-id="84a78-159">b.</span></span> <span data-ttu-id="84a78-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="84a78-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="84a78-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="84a78-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="84a78-163">W hello **przekazywania stanu** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="84a78-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84a78-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="84a78-164">These values are not real.</span></span> <span data-ttu-id="84a78-165">Rzeczywisty adres URL odpowiedzi i przekazywania stan hello zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="84a78-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="84a78-166">Skontaktuj się z [zespołem pomocy technicznej klienta maszyn wirtualnych IQNavigator](https://www.beeline.com/iqn-product-support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="84a78-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="84a78-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="84a78-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84a78-169">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="84a78-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="84a78-170">a.</span><span class="sxs-lookup"><span data-stu-id="84a78-170">a.</span></span> <span data-ttu-id="84a78-171">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="84a78-171">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="84a78-173">b.</span><span class="sxs-lookup"><span data-stu-id="84a78-173">b.</span></span> <span data-ttu-id="84a78-174">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="84a78-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="84a78-176">c.</span><span class="sxs-lookup"><span data-stu-id="84a78-176">c.</span></span> <span data-ttu-id="84a78-177">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="84a78-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="84a78-179">d.</span><span class="sxs-lookup"><span data-stu-id="84a78-179">d.</span></span> <span data-ttu-id="84a78-180">Teraz przejdź strony właściwości toohello **IQNavigator maszyn wirtualnych** i hello kopiowania **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="84a78-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="84a78-182">e.</span><span class="sxs-lookup"><span data-stu-id="84a78-182">e.</span></span> <span data-ttu-id="84a78-183">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="84a78-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="84a78-184">Aplikacja IQNavigator oczekiwać, że wartość identyfikatora unikatowego użytkownika hello hello oświadczenie identyfikatora nazwy.</span><span class="sxs-lookup"><span data-stu-id="84a78-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="84a78-185">Klienta można mapować hello poprawną wartość oświadczenia identyfikatora nazwy hello.</span><span class="sxs-lookup"><span data-stu-id="84a78-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="84a78-186">W takim przypadku zamapowaniu firma Microsoft hello użytkownika. UserPrincipalName w celu pokaz hello.</span><span class="sxs-lookup"><span data-stu-id="84a78-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="84a78-187">Jednak zgodnie z tooyour ustawienia organizacji należy mapować hello poprawną wartość dla niego.</span><span class="sxs-lookup"><span data-stu-id="84a78-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="84a78-189">Na powitania **konfiguracji maszyn wirtualnych IQNavigator** kliknij **Konfigurowanie maszyn wirtualnych IQNavigator** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="84a78-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84a78-190">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="84a78-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="84a78-192">tooconfigure rejestracji jednokrotnej w **maszyn wirtualnych IQNavigator** obok siebie, potrzebujesz toosend hello **adres URL metadanych**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** zbyt [IQNavigator maszyn wirtualnych z pomocą techniczną](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="84a78-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="84a78-193">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="84a78-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="84a78-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="84a78-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84a78-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="84a78-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84a78-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84a78-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84a78-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="84a78-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="84a78-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="84a78-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="84a78-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="84a78-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84a78-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="84a78-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84a78-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="84a78-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84a78-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84a78-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="84a78-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84a78-209">a.</span><span class="sxs-lookup"><span data-stu-id="84a78-209">a.</span></span> <span data-ttu-id="84a78-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84a78-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84a78-211">b.</span><span class="sxs-lookup"><span data-stu-id="84a78-211">b.</span></span> <span data-ttu-id="84a78-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="84a78-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84a78-213">c.</span><span class="sxs-lookup"><span data-stu-id="84a78-213">c.</span></span> <span data-ttu-id="84a78-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="84a78-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84a78-215">d.</span><span class="sxs-lookup"><span data-stu-id="84a78-215">d.</span></span> <span data-ttu-id="84a78-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="84a78-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="84a78-217">Tworzenie użytkownika testowego IQNavigator maszyny Wirtualne</span><span class="sxs-lookup"><span data-stu-id="84a78-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="84a78-218">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w IQNavigator maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84a78-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="84a78-219">Praca z [IQNavigator maszyn wirtualnych z pomocą techniczną](https://www.beeline.com/iqn-product-support/) tooadd hello użytkowników w hello konta IQNavigator maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84a78-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="84a78-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="84a78-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="84a78-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIQNavigator maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84a78-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="84a78-223">**tooassign tooIQNavigator Simona Britta maszyn wirtualnych, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="84a78-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="84a78-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="84a78-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="84a78-226">Z listy aplikacji hello wybierz **maszyn wirtualnych IQNavigator**.</span><span class="sxs-lookup"><span data-stu-id="84a78-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="84a78-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="84a78-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="84a78-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="84a78-230">Click **Add** button.</span></span> <span data-ttu-id="84a78-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="84a78-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="84a78-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84a78-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84a78-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="84a78-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84a78-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="84a78-236">Testing single sign-on</span></span>

<span data-ttu-id="84a78-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="84a78-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84a78-238">Po kliknięciu hello kafelka IQNavigator maszyn wirtualnych w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji IQNavigator maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="84a78-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="84a78-239">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84a78-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84a78-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="84a78-240">Additional resources</span></span>

* [<span data-ttu-id="84a78-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84a78-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84a78-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84a78-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

