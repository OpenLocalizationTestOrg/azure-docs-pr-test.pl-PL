---
title: 'Samouczek: Integracji Azure Active Directory z 23 wideo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i 23 wideo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="4caa2-103">Samouczek: Integracji Azure Active Directory z 23 wideo</span><span class="sxs-lookup"><span data-stu-id="4caa2-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="4caa2-104">Z tego samouczka, dowiesz się, jak toointegrate 23 wideo w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4caa2-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4caa2-105">Integrowanie 23 wideo z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4caa2-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4caa2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do wideo too23</span><span class="sxs-lookup"><span data-stu-id="4caa2-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="4caa2-107">Umożliwia użytkownikom uzyskać tooautomatically zalogowane too23 wideo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4caa2-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4caa2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4caa2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4caa2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4caa2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4caa2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4caa2-110">Prerequisites</span></span>

<span data-ttu-id="4caa2-111">tooconfigure integracji usługi Azure AD z 23 wideo należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4caa2-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="4caa2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4caa2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4caa2-113">23 wideo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4caa2-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4caa2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4caa2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4caa2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4caa2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4caa2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4caa2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4caa2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4caa2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4caa2-118">Scenario description</span></span>
<span data-ttu-id="4caa2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4caa2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4caa2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4caa2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4caa2-121">Dodawanie 23 wideo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4caa2-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="4caa2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4caa2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="4caa2-123">Dodawanie 23 wideo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4caa2-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="4caa2-124">tooconfigure hello integracji 23 wideo w usłudze Azure Active Directory, należy tooadd 23 wideo z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4caa2-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4caa2-125">**Wykonaj wideo z galerii hello tooadd 23 hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4caa2-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4caa2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4caa2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4caa2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4caa2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4caa2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4caa2-133">W polu wyszukiwania hello wpisz **23 wideo**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-133">In hello search box, type **23 Video**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="4caa2-135">W panelu wyników hello, wybierz **23 wideo**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4caa2-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4caa2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4caa2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4caa2-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 23 wideo na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4caa2-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4caa2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello 23 wideo jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4caa2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="4caa2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w 23 wideo musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4caa2-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="4caa2-141">23 wideo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="4caa2-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4caa2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z 23 wideo, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4caa2-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4caa2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4caa2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4caa2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4caa2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4caa2-145">**[Tworzenie użytkownika testowego 23 wideo](#creating-a-23-video-test-user)**  -toohave odpowiednikiem Simona Britta 23 wideo, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4caa2-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4caa2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4caa2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4caa2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4caa2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4caa2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4caa2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4caa2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w 23 aplikacji wideo.</span><span class="sxs-lookup"><span data-stu-id="4caa2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="4caa2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z 23 wideo, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4caa2-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4caa2-151">W portalu Azure na powitania hello **23 wideo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4caa2-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4caa2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="4caa2-155">Na powitania **23 Video domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4caa2-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="4caa2-157">a.</span><span class="sxs-lookup"><span data-stu-id="4caa2-157">a.</span></span> <span data-ttu-id="4caa2-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="4caa2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="4caa2-159">b.</span><span class="sxs-lookup"><span data-stu-id="4caa2-159">b.</span></span> <span data-ttu-id="4caa2-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="4caa2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4caa2-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4caa2-161">These values are not real.</span></span> <span data-ttu-id="4caa2-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4caa2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4caa2-163">Skontaktuj się z [23 zespołem pomocy technicznej klienta wideo](mailto:support@23company.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4caa2-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4caa2-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4caa2-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="4caa2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4caa2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4caa2-168">Na powitania **23 konfiguracji wideo** kliknij **skonfigurować wideo 23** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4caa2-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4caa2-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4caa2-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="4caa2-171">tooconfigure rejestracji jednokrotnej w **23 wideo** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**za[23 zespołem pomocy technicznej wideo](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="4caa2-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="4caa2-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4caa2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4caa2-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4caa2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4caa2-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4caa2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4caa2-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4caa2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4caa2-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4caa2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4caa2-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4caa2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4caa2-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4caa2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4caa2-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4caa2-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4caa2-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4caa2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4caa2-187">a.</span><span class="sxs-lookup"><span data-stu-id="4caa2-187">a.</span></span> <span data-ttu-id="4caa2-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4caa2-189">b.</span><span class="sxs-lookup"><span data-stu-id="4caa2-189">b.</span></span> <span data-ttu-id="4caa2-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4caa2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4caa2-191">c.</span><span class="sxs-lookup"><span data-stu-id="4caa2-191">c.</span></span> <span data-ttu-id="4caa2-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4caa2-193">d.</span><span class="sxs-lookup"><span data-stu-id="4caa2-193">d.</span></span> <span data-ttu-id="4caa2-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="4caa2-195">Tworzenie użytkownika testowego 23 wideo</span><span class="sxs-lookup"><span data-stu-id="4caa2-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="4caa2-196">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta 23 wideo.</span><span class="sxs-lookup"><span data-stu-id="4caa2-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="4caa2-197">**toocreate użytkownika o nazwie Simona Britta 23 wideo, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4caa2-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4caa2-198">Rejestracja tooyour 23 witryny firmy wideo jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4caa2-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="4caa2-199">Przejdź za**ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="4caa2-200">W **użytkowników** kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-200">In **Users** section, click **Configure**.</span></span>
   
    ![Przypisz użytkownika][400]

4. <span data-ttu-id="4caa2-202">Kliknij przycisk **dodać nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-202">Click **Add a new user**.</span></span> 
   
    ![Przypisz użytkownika][401]

5. <span data-ttu-id="4caa2-204">W hello **Poproś kogoś toojoin tej lokacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4caa2-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Przypisz użytkownika][402]

    <span data-ttu-id="4caa2-206">a.</span><span class="sxs-lookup"><span data-stu-id="4caa2-206">a.</span></span> <span data-ttu-id="4caa2-207">W hello **adresy E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4caa2-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="4caa2-208">b.</span><span class="sxs-lookup"><span data-stu-id="4caa2-208">b.</span></span> <span data-ttu-id="4caa2-209">Kliknij przycisk **Dodaj użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4caa2-210">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4caa2-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4caa2-211">W tej sekcji, musisz włączyć Simona Britta toouse Azure logowania jednokrotnego za udzielanie dostępu too23 wideo.</span><span class="sxs-lookup"><span data-stu-id="4caa2-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4caa2-213">**tooassign Simona Britta too23 wideo, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4caa2-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4caa2-214">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4caa2-216">Z listy aplikacji hello wybierz **23 wideo**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-216">In hello applications list, select **23 Video**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="4caa2-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4caa2-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4caa2-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4caa2-220">Click **Add** button.</span></span> <span data-ttu-id="4caa2-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4caa2-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4caa2-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4caa2-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4caa2-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4caa2-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4caa2-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4caa2-226">Testing single sign-on</span></span>

<span data-ttu-id="4caa2-227">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4caa2-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4caa2-228">Po kliknięciu kafelka wideo hello 23 w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour 23 wideo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4caa2-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4caa2-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4caa2-229">Additional resources</span></span>

* [<span data-ttu-id="4caa2-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4caa2-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4caa2-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4caa2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
