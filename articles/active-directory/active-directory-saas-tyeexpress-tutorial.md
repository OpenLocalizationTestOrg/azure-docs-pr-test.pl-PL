---
title: 'Samouczek: Integracji Azure Active Directory z T & E Express | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="d1dd3-103">Samouczek: Integracji Azure Active Directory z T & E Express</span><span class="sxs-lookup"><span data-stu-id="d1dd3-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="d1dd3-104">Z tego samouczka, dowiesz się, jak toointegrate T & E Express z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1dd3-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1dd3-105">Integracja z usługą Azure AD T & E Express zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d1dd3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooT & E Express</span><span class="sxs-lookup"><span data-stu-id="d1dd3-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="d1dd3-107">Użytkownicy tooautomatically get zalogowane tooT & E Express (logowanie jednokrotne) można włączyć przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1dd3-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1dd3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="d1dd3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d1dd3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1dd3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1dd3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1dd3-110">Prerequisites</span></span>

<span data-ttu-id="d1dd3-111">tooconfigure integracji usługi Azure AD z T & E Express należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="d1dd3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1dd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1dd3-113">T & E Express jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d1dd3-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1dd3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1dd3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1dd3-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d1dd3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1dd3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1dd3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d1dd3-118">Scenario description</span></span>
<span data-ttu-id="d1dd3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1dd3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1dd3-121">Dodawanie T & E Express z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d1dd3-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="d1dd3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d1dd3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="d1dd3-123">Dodawanie T & E Express z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d1dd3-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="d1dd3-124">tooconfigure hello integracji T & E Express do usługi Azure AD, należy tooadd T & E Express z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d1dd3-125">**tooadd T & E Express z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d1dd3-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1dd3-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d1dd3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d1dd3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d1dd3-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d1dd3-133">W polu wyszukiwania hello wpisz **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-133">In hello search box, type **T&E Express**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="d1dd3-135">W panelu wyników hello zaznacz **T & E Express**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1dd3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d1dd3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1dd3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z T & E Express, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1dd3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w T & E Express jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="d1dd3-140">Innymi słowy link relację między użytkownika usługi Azure AD i hello użytkownikowi w T & E Express toobe potrzeb ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="d1dd3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **nazwy użytkownika** w T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="d1dd3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z T & E Express, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d1dd3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d1dd3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1dd3-145">**[Tworzenie użytkownika testowego T & E Express](#creating-a-te-express-test-user)**  -toohave odpowiednikiem Simona Britta w T & E Express, która jest jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d1dd3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1dd3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1dd3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d1dd3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1dd3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="d1dd3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z T & E Express, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d1dd3-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1dd3-151">W portalu zarządzania Azure hello na powitania **T & E Express** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d1dd3-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="d1dd3-155">Na powitania **& E Express domeny i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="d1dd3-157">a.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-157">a.</span></span> <span data-ttu-id="d1dd3-158">W hello **identyfikator** pole tekstowe, wartość hello typu jako:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="d1dd3-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="d1dd3-159">b.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-159">b.</span></span> <span data-ttu-id="d1dd3-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="d1dd3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1dd3-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d1dd3-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d1dd3-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d1dd3-164">Skontaktuj się z [T & E Express obsługują zespołu](http://www.tyeexpress.com/contacto.aspx) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="d1dd3-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="d1dd3-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d1dd3-169">tooconfigure rejestracji jednokrotnej w **T & E Express** po stronie, logowania toohello T & E express aplikacji bez SAML Rejestracja jednokrotna przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="d1dd3-170">W obszarze hello **Admin** kliknij **domeny SAML** tooOpen hello SAML ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="d1dd3-172">Wybierz hello **Activar(Activate)** opcję **nr** za**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="d1dd3-173">W hello **metadanych dostawcy tożsamości** pole tekstowe, metadane hello Wklej kod XML, który ma donwloaded z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="d1dd3-175">Polecenie hello **Guardar(Save)** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1dd3-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1dd3-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1dd3-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d1dd3-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d1dd3-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1dd3-180">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1dd3-182">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1dd3-184">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1dd3-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d1dd3-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1dd3-188">a.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-188">a.</span></span> <span data-ttu-id="d1dd3-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1dd3-190">b.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-190">b.</span></span> <span data-ttu-id="d1dd3-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1dd3-192">c.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-192">c.</span></span> <span data-ttu-id="d1dd3-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d1dd3-194">d.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-194">d.</span></span> <span data-ttu-id="d1dd3-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="d1dd3-196">Tworzenie użytkownika testowego T & E Express</span><span class="sxs-lookup"><span data-stu-id="d1dd3-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="d1dd3-197">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do T & E Express muszą mieć przydzielone do T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="d1dd3-198">W przypadku T & E Express Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="d1dd3-199">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d1dd3-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1dd3-200">Zaloguj się za tooyour T & E Express witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="d1dd3-201">W obszarze tagu administratora kliknij na stronie wzorcowej użytkowników hello tooopen użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="d1dd3-203">Na stronie głównej powitania kliknij  **+**  tooadd hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="d1dd3-205">Wszystkie szczegóły obowiązkowe hello jako zadawane w postaci hello i kliknij przycisk hello Zapisz szczegóły hello toosave przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Dodawanie pracownika](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d1dd3-208">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1dd3-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d1dd3-209">W tej sekcji można włączyć toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej dostępu tooT & E Express.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d1dd3-211">**tooassign tooT Simona Britta & E Express, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d1dd3-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1dd3-212">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d1dd3-214">Z listy aplikacji hello wybierz **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-214">In hello applications list, select **T&E Express**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="d1dd3-216">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d1dd3-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-218">Click **Add** button.</span></span> <span data-ttu-id="d1dd3-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d1dd3-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d1dd3-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1dd3-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1dd3-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d1dd3-224">Testing single sign-on</span></span>

<span data-ttu-id="d1dd3-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d1dd3-226">Po kliknięciu hello T & E Express kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour T & E Express aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1dd3-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1dd3-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d1dd3-227">Additional resources</span></span>

* [<span data-ttu-id="d1dd3-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1dd3-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1dd3-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1dd3-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

