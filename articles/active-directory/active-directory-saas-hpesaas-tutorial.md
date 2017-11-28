---
title: 'Samouczek: Integracji Azure Active Directory z HPE SaaS | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i HPE SaaS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 7a846fb2298e51d249f4a406527130828bf7bbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="1a2e3-103">Samouczek: Integracji Azure Active Directory z HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="1a2e3-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="1a2e3-104">Z tego samouczka, dowiesz się, jak toointegrate HPE SaaS w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a2e3-104">In this tutorial, you learn how toointegrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a2e3-105">Integracja z usługą Azure AD HPE SaaS zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-105">Integrating HPE SaaS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a2e3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHPE SaaS</span><span class="sxs-lookup"><span data-stu-id="1a2e3-106">You can control in Azure AD who has access tooHPE SaaS</span></span>
- <span data-ttu-id="1a2e3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHPE SaaS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2e3-107">You can enable your users tooautomatically get signed-on tooHPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a2e3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1a2e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1a2e3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a2e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a2e3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a2e3-110">Prerequisites</span></span>

<span data-ttu-id="1a2e3-111">tooconfigure integracji usługi Azure AD z HPE SaaS należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-111">tooconfigure Azure AD integration with HPE SaaS, you need hello following items:</span></span>

- <span data-ttu-id="1a2e3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a2e3-113">HPE SaaS logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1a2e3-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a2e3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a2e3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a2e3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a2e3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a2e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a2e3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1a2e3-118">Scenario description</span></span>
<span data-ttu-id="1a2e3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a2e3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a2e3-121">Dodawanie HPE SaaS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1a2e3-121">Adding HPE SaaS from hello gallery</span></span>
2. <span data-ttu-id="1a2e3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1a2e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-hello-gallery"></a><span data-ttu-id="1a2e3-123">Dodawanie HPE SaaS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1a2e3-123">Adding HPE SaaS from hello gallery</span></span>
<span data-ttu-id="1a2e3-124">tooconfigure hello integracji HPE SaaS w usłudze Azure Active Directory, należy tooadd HPE SaaS z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-124">tooconfigure hello integration of HPE SaaS into Azure AD, you need tooadd HPE SaaS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a2e3-125">**tooadd SaaS HPE z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1a2e3-125">**tooadd HPE SaaS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a2e3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1a2e3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a2e3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1a2e3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1a2e3-133">W polu wyszukiwania hello wpisz **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-133">In hello search box, type **HPE SaaS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="1a2e3-135">W panelu wyników hello, wybierz **HPE SaaS**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-135">In hello results panel, select **HPE SaaS**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a2e3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1a2e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a2e3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SaaS HPE w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a2e3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w modelu SaaS HPE jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HPE SaaS is tooa user in Azure AD.</span></span> <span data-ttu-id="1a2e3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w modelu SaaS HPE musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-140">In other words, a link relationship between an Azure AD user and hello related user in HPE SaaS needs toobe established.</span></span>

<span data-ttu-id="1a2e3-141">W modelu SaaS HPE, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-141">In HPE SaaS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1a2e3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z HPE SaaS, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-142">tooconfigure and test Azure AD single sign-on with HPE SaaS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a2e3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a2e3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a2e3-145">**[Tworzenie użytkownika testowego HPE SaaS](#creating-an-hpe-saas-test-user)**  -toohave odpowiednikiem Simona Britta w modelu SaaS HPE, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - toohave a counterpart of Britta Simon in HPE SaaS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a2e3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a2e3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a2e3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a2e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a2e3-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne do aplikacji HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="1a2e3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z HPE SaaS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1a2e3-150">**tooconfigure Azure AD single sign-on with HPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a2e3-151">W portalu Azure na powitania hello **HPE SaaS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-151">In hello Azure portal, on hello **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1a2e3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="1a2e3-155">Na powitania **HPE SaaS domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-155">On hello **HPE SaaS Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="1a2e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-157">a.</span></span> <span data-ttu-id="1a2e3-158">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="1a2e3-158">In hello **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="1a2e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-159">b.</span></span> <span data-ttu-id="1a2e3-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="1a2e3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a2e3-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-161">These values are not real.</span></span> <span data-ttu-id="1a2e3-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a2e3-163">Skontaktuj się z [zespołem pomocy technicznej klienta SaaS HPE](https://saas.hpe.com/en-us/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="1a2e3-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="1a2e3-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a2e3-168">tooconfigure rejestracji jednokrotnej w **HPE SaaS** strony, należy pobrać hello toosend **XML metadanych** za[HPE SaaS obsługuje zespołu](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="1a2e3-168">tooconfigure single sign-on on **HPE SaaS** side, you need toosend hello downloaded **Metadata XML** too[HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="1a2e3-169">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1a2e3-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="1a2e3-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1a2e3-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1a2e3-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a2e3-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a2e3-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2e3-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a2e3-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1a2e3-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1a2e3-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a2e3-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a2e3-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a2e3-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a2e3-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1a2e3-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a2e3-185">a.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-185">a.</span></span> <span data-ttu-id="1a2e3-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a2e3-187">b.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-187">b.</span></span> <span data-ttu-id="1a2e3-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a2e3-189">c.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-189">c.</span></span> <span data-ttu-id="1a2e3-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a2e3-191">d.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-191">d.</span></span> <span data-ttu-id="1a2e3-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="1a2e3-193">Tworzenie użytkownika testowego HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="1a2e3-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="1a2e3-194">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-194">hello objective of this section is toocreate a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="1a2e3-195">We współpracy z [HPE SaaS obsługuje zespołu](https://saas.hpe.com/en-us/contact) tooadd hello użytkowników w hello HPE SaaS konta.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) tooadd hello users in hello HPE SaaS account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a2e3-196">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2e3-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a2e3-197">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHPE SaaS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1a2e3-199">**tooassign tooHPE Simona Britta SaaS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1a2e3-199">**tooassign Britta Simon tooHPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a2e3-200">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1a2e3-202">Z listy aplikacji hello wybierz **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-202">In hello applications list, select **HPE SaaS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="1a2e3-204">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1a2e3-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-206">Click **Add** button.</span></span> <span data-ttu-id="1a2e3-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1a2e3-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a2e3-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a2e3-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a2e3-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a2e3-212">Testing single sign-on</span></span>

<span data-ttu-id="1a2e3-213">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1a2e3-214">Po kliknięciu powitalne HPE SaaS kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a2e3-214">When you click hello HPE SaaS tile in hello Access Panel, you should get automatically signed-on tooyour HPE SaaS application.</span></span>
<span data-ttu-id="1a2e3-215">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a2e3-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a2e3-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1a2e3-216">Additional resources</span></span>

* [<span data-ttu-id="1a2e3-217">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a2e3-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a2e3-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a2e3-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

