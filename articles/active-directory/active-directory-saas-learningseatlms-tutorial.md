---
title: 'Samouczek: Integracji Azure Active Directory z LMS stanowisko Learning | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LMS stanowisko Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="a65a3-103">Samouczek: Integracji Azure Active Directory z LMS stanowisko Learning</span><span class="sxs-lookup"><span data-stu-id="a65a3-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="a65a3-104">Z tego samouczka, dowiesz się, jak toointegrate LMS stanowisko Learning z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a65a3-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a65a3-105">Integrowanie LMS stanowisko Learning z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a65a3-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a65a3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLearning LMS stanowisko</span><span class="sxs-lookup"><span data-stu-id="a65a3-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="a65a3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLearning LMS stanowisko (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a65a3-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a65a3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a65a3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a65a3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="a65a3-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a65a3-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a65a3-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a65a3-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a65a3-111">Prerequisites</span></span>

<span data-ttu-id="a65a3-112">tooconfigure integracji usługi Azure AD z LMS stanowisko Learning należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a65a3-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="a65a3-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a65a3-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a65a3-114">Learning stanowisko LMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a65a3-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a65a3-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a65a3-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a65a3-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a65a3-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a65a3-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a65a3-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a65a3-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a65a3-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a65a3-119">Scenario description</span></span>
<span data-ttu-id="a65a3-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a65a3-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a65a3-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a65a3-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a65a3-122">Dodawanie LMS stanowisko Learning z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a65a3-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="a65a3-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a65a3-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="a65a3-124">Dodawanie LMS stanowisko Learning z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a65a3-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="a65a3-125">tooconfigure hello integracji LMS stanowisko Learning z usługą Azure AD, należy tooadd LMS stanowisko Learning z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a65a3-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a65a3-126">**tooadd LMS stanowisko Learning z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a65a3-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a65a3-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a65a3-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a65a3-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a65a3-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a65a3-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a65a3-134">W polu wyszukiwania hello wpisz **LMS stanowisko Learning**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="a65a3-136">W panelu wyników hello, wybierz **LMS stanowisko Learning**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a65a3-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a65a3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a65a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a65a3-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LMS stanowisko uczenie na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a65a3-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a65a3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LMS stanowisko Learning jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a65a3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="a65a3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LMS stanowisko Learning musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a65a3-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="a65a3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="a65a3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="a65a3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Learning stanowisko LMS, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a65a3-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a65a3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a65a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a65a3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a65a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a65a3-145">**[Tworzenie użytkownika testowego LMS stanowisko Learning](#creating-a-learnconnect-test-user)**  -toohave odpowiednikiem Simona Britta w LMS stanowisko Learning, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a65a3-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a65a3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a65a3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a65a3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a65a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a65a3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a65a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a65a3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="a65a3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="a65a3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Learning stanowisko LMS, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a65a3-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="a65a3-151">W portalu Azure na powitania hello **LMS stanowisko Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a65a3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a65a3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="a65a3-155">Na powitania **Learning stanowisko LMS domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a65a3-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="a65a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="a65a3-157">a.</span></span> <span data-ttu-id="a65a3-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="a65a3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="a65a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="a65a3-159">b.</span></span> <span data-ttu-id="a65a3-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="a65a3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="a65a3-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a65a3-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="a65a3-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="a65a3-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a65a3-164">Wartości te nie są hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="a65a3-164">These values are not hello real values.</span></span> <span data-ttu-id="a65a3-165">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="a65a3-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a65a3-166">Skontaktuj się z [zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a65a3-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="a65a3-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a65a3-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="a65a3-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a65a3-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a65a3-171">tooconfigure rejestracji jednokrotnej w **LMS stanowisko Learning** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="a65a3-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="a65a3-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a65a3-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a65a3-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a65a3-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a65a3-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a65a3-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a65a3-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a65a3-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="a65a3-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a65a3-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a65a3-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a65a3-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a65a3-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a65a3-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a65a3-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a65a3-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a65a3-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a65a3-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a65a3-187">a.</span><span class="sxs-lookup"><span data-stu-id="a65a3-187">a.</span></span> <span data-ttu-id="a65a3-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a65a3-189">b.</span><span class="sxs-lookup"><span data-stu-id="a65a3-189">b.</span></span> <span data-ttu-id="a65a3-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a65a3-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a65a3-191">c.</span><span class="sxs-lookup"><span data-stu-id="a65a3-191">c.</span></span> <span data-ttu-id="a65a3-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a65a3-193">d.</span><span class="sxs-lookup"><span data-stu-id="a65a3-193">d.</span></span> <span data-ttu-id="a65a3-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="a65a3-195">Tworzenie użytkownika testowego LMS stanowisko Learning</span><span class="sxs-lookup"><span data-stu-id="a65a3-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="a65a3-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w LMS stanowisko Learning.</span><span class="sxs-lookup"><span data-stu-id="a65a3-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="a65a3-197">Skontaktuj się z [zespołem pomocy technicznej stanowisko Learning](http://help.learningseatlms.com/help) wszystkie hello użytkownika informacje tooadd hello użytkownikom z hello LMS stanowisko Learning aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a65a3-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a65a3-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a65a3-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a65a3-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLearning LMS stanowisko.</span><span class="sxs-lookup"><span data-stu-id="a65a3-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a65a3-201">**tooassign tooLearning Simona Britta LMS stanowisko, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a65a3-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="a65a3-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a65a3-204">Z listy aplikacji hello wybierz **LMS stanowisko Learning**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="a65a3-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a65a3-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a65a3-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a65a3-208">Click **Add** button.</span></span> <span data-ttu-id="a65a3-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a65a3-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a65a3-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a65a3-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a65a3-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a65a3-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a65a3-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a65a3-214">Testing single sign-on</span></span>

<span data-ttu-id="a65a3-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a65a3-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="a65a3-216">Kliknij przycisk hello LMS stanowisko Learning kafelka w hello panelu dostępu będzie automatycznie zalogowane tooyour LMS stanowisko Learning aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a65a3-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="a65a3-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a65a3-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a65a3-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a65a3-218">Additional resources</span></span>

* [<span data-ttu-id="a65a3-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a65a3-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a65a3-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a65a3-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

