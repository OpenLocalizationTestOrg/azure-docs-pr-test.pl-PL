---
title: 'Samouczek: Integracji Azure Active Directory osobom | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i osoby."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="ec1de-103">Samouczek: Integracji Azure Active Directory osobom</span><span class="sxs-lookup"><span data-stu-id="ec1de-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="ec1de-104">Z tego samouczka, dowiesz się, jak toointegrate osoby z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec1de-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec1de-105">Integrowanie osób z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ec1de-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec1de-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPeople</span><span class="sxs-lookup"><span data-stu-id="ec1de-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="ec1de-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPeople (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec1de-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec1de-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ec1de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec1de-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec1de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec1de-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ec1de-110">Prerequisites</span></span>

<span data-ttu-id="ec1de-111">tooconfigure integracji z usługą Azure AD osobom należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ec1de-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="ec1de-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec1de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec1de-113">Osoby logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ec1de-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec1de-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec1de-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ec1de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec1de-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ec1de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec1de-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec1de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec1de-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ec1de-118">Scenario description</span></span>
<span data-ttu-id="ec1de-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ec1de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec1de-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ec1de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec1de-121">Dodawanie użytkowników z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ec1de-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="ec1de-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ec1de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="ec1de-123">Dodawanie użytkowników z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ec1de-123">Adding People from hello gallery</span></span>
<span data-ttu-id="ec1de-124">tooconfigure hello integracji osób do usługi Azure AD, należy tooadd osób z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ec1de-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec1de-125">**tooadd osób z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ec1de-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec1de-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ec1de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ec1de-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec1de-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ec1de-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ec1de-133">W polu wyszukiwania hello wpisz **osób**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-133">In hello search box, type **People**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="ec1de-135">W panelu wyników hello, wybierz **osób**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ec1de-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec1de-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ec1de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec1de-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej osobom w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec1de-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w osób jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec1de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="ec1de-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w osób musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ec1de-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="ec1de-141">Osoby, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ec1de-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec1de-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej osobom, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ec1de-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec1de-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ec1de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec1de-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ec1de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec1de-145">**[Tworzenie użytkownika testowego osób](#creating-a-people-test-user)**  -toohave odpowiednikiem Simona Britta w osób, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ec1de-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec1de-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ec1de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec1de-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ec1de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec1de-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ec1de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec1de-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji osób.</span><span class="sxs-lookup"><span data-stu-id="ec1de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="ec1de-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej osobom, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ec1de-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec1de-151">W portalu Azure na powitania hello **osób** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ec1de-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ec1de-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="ec1de-155">Na powitania **domeny osoby i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ec1de-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="ec1de-157">a.</span><span class="sxs-lookup"><span data-stu-id="ec1de-157">a.</span></span> <span data-ttu-id="ec1de-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="ec1de-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="ec1de-159">b.</span><span class="sxs-lookup"><span data-stu-id="ec1de-159">b.</span></span> <span data-ttu-id="ec1de-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="ec1de-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="ec1de-161">c.</span><span class="sxs-lookup"><span data-stu-id="ec1de-161">c.</span></span> <span data-ttu-id="ec1de-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="ec1de-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec1de-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ec1de-163">These values are not real.</span></span> <span data-ttu-id="ec1de-164">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ec1de-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ec1de-165">Skontaktuj się z [zespołem pomocy technicznej klienta osób](mailto:customerservices@peoplehr.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ec1de-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="ec1de-166">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ec1de-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="ec1de-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ec1de-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ec1de-170">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour osób dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="ec1de-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="ec1de-171">W menu powitania po lewej stronie powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="ec1de-173">Kliknij przycisk **firmy**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-173">Click **Company**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="ec1de-175">Na powitania **pliku metadanych przekazywania "Rejestracji jednokrotnej" SAML**, kliknij przycisk **Przeglądaj** tooupload hello pobrany plik metadanych.</span><span class="sxs-lookup"><span data-stu-id="ec1de-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="ec1de-177">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ec1de-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec1de-178">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ec1de-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec1de-179">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec1de-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec1de-180">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec1de-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec1de-181">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ec1de-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ec1de-183">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ec1de-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec1de-184">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ec1de-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec1de-186">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec1de-188">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec1de-190">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ec1de-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec1de-192">a.</span><span class="sxs-lookup"><span data-stu-id="ec1de-192">a.</span></span> <span data-ttu-id="ec1de-193">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec1de-194">b.</span><span class="sxs-lookup"><span data-stu-id="ec1de-194">b.</span></span> <span data-ttu-id="ec1de-195">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec1de-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec1de-196">c.</span><span class="sxs-lookup"><span data-stu-id="ec1de-196">c.</span></span> <span data-ttu-id="ec1de-197">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec1de-198">d.</span><span class="sxs-lookup"><span data-stu-id="ec1de-198">d.</span></span> <span data-ttu-id="ec1de-199">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="ec1de-200">Tworzenie użytkownika testowego osób</span><span class="sxs-lookup"><span data-stu-id="ec1de-200">Creating a People test user</span></span>

<span data-ttu-id="ec1de-201">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w osób.</span><span class="sxs-lookup"><span data-stu-id="ec1de-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="ec1de-202">Praca z [zespołem pomocy technicznej klienta osób](mailto:customerservices@peoplehr.com) do dodawania użytkowników hello hello osób platformy.</span><span class="sxs-lookup"><span data-stu-id="ec1de-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="ec1de-203">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ec1de-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec1de-204">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec1de-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec1de-205">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPeople.</span><span class="sxs-lookup"><span data-stu-id="ec1de-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ec1de-207">**tooassign tooPeople Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ec1de-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec1de-208">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ec1de-210">Z listy aplikacji hello wybierz **osób**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-210">In hello applications list, select **People**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="ec1de-212">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ec1de-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ec1de-214">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ec1de-214">Click **Add** button.</span></span> <span data-ttu-id="ec1de-215">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ec1de-217">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ec1de-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec1de-218">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec1de-219">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ec1de-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec1de-220">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ec1de-220">Testing single sign-on</span></span>

<span data-ttu-id="ec1de-221">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ec1de-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec1de-222">Po kliknięciu powitalne osób kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour osób aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec1de-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec1de-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ec1de-223">Additional resources</span></span>

* [<span data-ttu-id="ec1de-224">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec1de-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec1de-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec1de-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

