---
title: "Samouczek: Integracji Azure Active Directory z urzędu certyfikacji PPM | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PPM urzędu certyfikacji."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="2ed4b-103">Samouczek: Integracji Azure Active Directory z PPM urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="2ed4b-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="2ed4b-104">Z tego samouczka, dowiesz się, jak toointegrate PPM urzędu certyfikacji w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ed4b-105">Integrowanie PPM urzędu certyfikacji z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ed4b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCA PPM</span><span class="sxs-lookup"><span data-stu-id="2ed4b-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="2ed4b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCA PPM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ed4b-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ed4b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2ed4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ed4b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ed4b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ed4b-110">Prerequisites</span></span>

<span data-ttu-id="2ed4b-111">tooconfigure integracji usługi Azure AD z PPM urzędu certyfikacji należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="2ed4b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ed4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ed4b-113">Urząd certyfikacji PPM jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2ed4b-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ed4b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ed4b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ed4b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ed4b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ed4b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2ed4b-118">Scenario description</span></span>
<span data-ttu-id="2ed4b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ed4b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ed4b-121">Dodawanie PPM urzędu certyfikacji z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2ed4b-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="2ed4b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2ed4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="2ed4b-123">Dodawanie PPM urzędu certyfikacji z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2ed4b-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="2ed4b-124">tooconfigure hello integracji PPM urzędu certyfikacji w usłudze Azure Active Directory, należy tooadd PPM urzędu certyfikacji z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ed4b-125">**tooadd PPM urzędu certyfikacji z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2ed4b-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ed4b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2ed4b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ed4b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2ed4b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2ed4b-133">W polu wyszukiwania hello wpisz **PPM urzędu certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-133">In hello search box, type **CA PPM**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="2ed4b-135">W panelu wyników hello zaznacz **PPM urzędu certyfikacji**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ed4b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2ed4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ed4b-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PPM urzędu certyfikacji, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2ed4b-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ed4b-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PPM urzędu certyfikacji jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="2ed4b-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PPM urzędu certyfikacji musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="2ed4b-141">W PPM urzędu certyfikacji, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ed4b-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PPM urzędu certyfikacji, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ed4b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ed4b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ed4b-145">**[Tworzenie użytkownika testowego urzędu certyfikacji PPM](#creating-a-ca-ppm-test-user)**  -toohave odpowiednikiem Simona Britta w PPM urzędu certyfikacji, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ed4b-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ed4b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ed4b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2ed4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ed4b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji PPM urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="2ed4b-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PPM urzędu certyfikacji, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2ed4b-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ed4b-151">W portalu Azure na powitania hello **PPM urzędu certyfikacji** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2ed4b-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="2ed4b-155">Na powitania **domeny PPM urzędu certyfikacji i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="2ed4b-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-157">a.</span></span> <span data-ttu-id="2ed4b-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="2ed4b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="2ed4b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-159">b.</span></span> <span data-ttu-id="2ed4b-160">W hello **adres URL odpowiedzi** pole tekstowe, typu co:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="2ed4b-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ed4b-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-161">This value is not real.</span></span> <span data-ttu-id="2ed4b-162">Zaktualizuj tę wartość z hello rzeczywisty identyfikator.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="2ed4b-163">Skontaktuj się z [zespołem pomocy technicznej PPM urzędu certyfikacji](mailto:catechnicalsupport@ca.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="2ed4b-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="2ed4b-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ed4b-168">Na powitania **konfiguracji urzędu certyfikacji PPM** , kliknij przycisk **skonfigurować urząd certyfikacji PPM** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ed4b-169">Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2ed4b-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="2ed4b-171">tooconfigure rejestracji jednokrotnej w **PPM urzędu certyfikacji** strony, należy pobrać hello toosend **Certificate(Base64)** i **identyfikator jednostki SAML** zbyt[zespołem pomocy technicznej PPM urzędu certyfikacji ](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="2ed4b-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="2ed4b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ed4b-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ed4b-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ed4b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ed4b-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ed4b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ed4b-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2ed4b-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2ed4b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ed4b-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ed4b-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ed4b-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ed4b-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ed4b-187">a.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-187">a.</span></span> <span data-ttu-id="2ed4b-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ed4b-189">b.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-189">b.</span></span> <span data-ttu-id="2ed4b-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ed4b-191">c.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-191">c.</span></span> <span data-ttu-id="2ed4b-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ed4b-193">d.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-193">d.</span></span> <span data-ttu-id="2ed4b-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="2ed4b-195">Tworzenie użytkownika testowego PPM urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="2ed4b-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="2ed4b-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w PPM urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="2ed4b-197">Praca z [zespołem pomocy technicznej PPM urzędu certyfikacji](mailto:catechnicalsupport@ca.com) użytkowników hello tooadd hello platformy PPM urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2ed4b-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ed4b-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2ed4b-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCA PPM.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2ed4b-201">**tooassign tooCA Simona Britta PPM, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2ed4b-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ed4b-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2ed4b-204">Z listy aplikacji hello wybierz **PPM urzędu certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-204">In hello applications list, select **CA PPM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="2ed4b-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2ed4b-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-208">Click **Add** button.</span></span> <span data-ttu-id="2ed4b-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2ed4b-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ed4b-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ed4b-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ed4b-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2ed4b-214">Testing single sign-on</span></span>

<span data-ttu-id="2ed4b-215">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ed4b-216">Po kliknięciu kafelka PPM urzędu certyfikacji hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PPM urzędu certyfikacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ed4b-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2ed4b-217">Additional resources</span></span>

* [<span data-ttu-id="2ed4b-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ed4b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ed4b-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ed4b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

