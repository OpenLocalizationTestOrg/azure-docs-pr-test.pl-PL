---
title: 'Samouczek: Azure Active Directory integracji z programem SAP NetWeaver | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="51261-103">Samouczek: integracja usługi Azure Active Directory z oprogramowaniem SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="51261-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="51261-104">Z tego samouczka, dowiesz się, jak toointegrate SAP NetWeaver w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51261-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51261-105">Integrowanie programu SAP NetWeaver z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="51261-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="51261-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="51261-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="51261-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP NetWeaver (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="51261-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51261-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="51261-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="51261-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51261-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="51261-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51261-110">Prerequisites</span></span>

<span data-ttu-id="51261-111">tooconfigure integracji z usługą Azure AD z programem SAP NetWeaver należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="51261-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="51261-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="51261-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51261-113">SAP NetWeaver jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="51261-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51261-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="51261-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51261-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="51261-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51261-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="51261-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51261-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51261-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51261-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="51261-118">Scenario description</span></span>
<span data-ttu-id="51261-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="51261-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51261-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="51261-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51261-121">Dodawanie programem SAP NetWeaver z galerii hello</span><span class="sxs-lookup"><span data-stu-id="51261-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="51261-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="51261-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="51261-123">Dodawanie programem SAP NetWeaver z galerii hello</span><span class="sxs-lookup"><span data-stu-id="51261-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="51261-124">tooconfigure hello integracji z programem SAP NetWeaver w usłudze Azure Active Directory, należy tooadd SAP NetWeaver z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="51261-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="51261-125">**tooadd SAP NetWeaver z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="51261-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="51261-126">W hello  **[Azure Portal](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="51261-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="51261-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="51261-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="51261-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="51261-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="51261-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51261-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="51261-133">W polu wyszukiwania hello wpisz **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="51261-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="51261-135">W panelu wyników hello zaznacz **SAP NetWeaver**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="51261-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51261-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="51261-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51261-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z programem SAP NetWeaver oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="51261-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51261-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP NetWeaver jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51261-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="51261-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SAP NetWeaver musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="51261-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="51261-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="51261-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="51261-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z programem SAP NetWeaver, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="51261-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="51261-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="51261-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="51261-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="51261-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51261-145">**[Tworzenie użytkownika testowego SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave odpowiednikiem Simona Britta w SAP NetWeaver, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51261-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="51261-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="51261-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51261-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="51261-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51261-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="51261-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51261-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="51261-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="51261-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z programem SAP NetWeaver wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="51261-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="51261-151">W portalu Azure na powitania hello **SAP NetWeaver** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="51261-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="51261-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="51261-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="51261-155">Na powitania **adresy URL i SAP NetWeaver domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="51261-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="51261-157">a.</span><span class="sxs-lookup"><span data-stu-id="51261-157">a.</span></span> <span data-ttu-id="51261-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="51261-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="51261-159">b.</span><span class="sxs-lookup"><span data-stu-id="51261-159">b.</span></span> <span data-ttu-id="51261-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="51261-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="51261-161">c.</span><span class="sxs-lookup"><span data-stu-id="51261-161">c.</span></span> <span data-ttu-id="51261-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="51261-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="51261-163">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="51261-163">These values are not hello real.</span></span> <span data-ttu-id="51261-164">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="51261-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="51261-165">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="51261-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="51261-166">Skontaktuj się z [zespołu pomocy technicznej programu SAP NetWeaver klienta](https://www.sap.com/support.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="51261-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="51261-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="51261-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="51261-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="51261-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="51261-171">Na powitania **SAP NetWeaver konfiguracji** kliknij **skonfigurować SAP NetWeaver** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="51261-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="51261-172">Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="51261-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="51261-174">tooconfigure rejestracji jednokrotnej w **SAP NetWeaver** strony, należy pobrać hello toosend **XML metadanych** i **identyfikator jednostki SAML** zbyt[SAP NetWeaver pomocy technicznej ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="51261-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="51261-175">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="51261-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="51261-176">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="51261-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="51261-177">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51261-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51261-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="51261-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="51261-179">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="51261-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="51261-181">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="51261-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="51261-182">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="51261-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51261-184">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="51261-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51261-186">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51261-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51261-188">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="51261-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51261-190">a.</span><span class="sxs-lookup"><span data-stu-id="51261-190">a.</span></span> <span data-ttu-id="51261-191">W hello **nazwa** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="51261-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="51261-192">b.</span><span class="sxs-lookup"><span data-stu-id="51261-192">b.</span></span> <span data-ttu-id="51261-193">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="51261-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="51261-194">c.</span><span class="sxs-lookup"><span data-stu-id="51261-194">c.</span></span> <span data-ttu-id="51261-195">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="51261-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="51261-196">d.</span><span class="sxs-lookup"><span data-stu-id="51261-196">d.</span></span> <span data-ttu-id="51261-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="51261-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="51261-198">Tworzenie użytkownika testowego SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="51261-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="51261-199">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="51261-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="51261-200">Praca z Twojej [Obsługa SAP NetWeaver](https://www.sap.com/support.html) tooadd hello użytkowników na platformie programu SAP NetWeaver hello.</span><span class="sxs-lookup"><span data-stu-id="51261-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="51261-201">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="51261-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="51261-202">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="51261-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="51261-204">**tooassign tooSAP Simona Britta NetWeaver, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="51261-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="51261-205">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="51261-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="51261-207">Z listy aplikacji hello wybierz **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="51261-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="51261-209">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="51261-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="51261-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="51261-211">Click **Add** button.</span></span> <span data-ttu-id="51261-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51261-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="51261-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="51261-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="51261-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51261-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51261-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51261-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51261-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="51261-217">Testing single sign-on</span></span>

<span data-ttu-id="51261-218">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="51261-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="51261-219">Po kliknięciu kafelka SAP NetWeaver hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SAP NetWeaver aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51261-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51261-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="51261-220">Additional resources</span></span>

* [<span data-ttu-id="51261-221">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51261-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51261-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51261-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

