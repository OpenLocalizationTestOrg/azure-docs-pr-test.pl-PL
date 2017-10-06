---
title: 'Samouczek: Integracji Azure Active Directory z TigerText Secure Messenger | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="d5426-103">Samouczek: Integracji Azure Active Directory z TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="d5426-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="d5426-104">Z tego samouczka, dowiesz się, jak toointegrate bezpiecznego TigerText Messenger w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5426-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5426-105">Integracja z usługą Azure AD TigerText Secure Messenger zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d5426-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5426-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTigerText bezpiecznego Messenger</span><span class="sxs-lookup"><span data-stu-id="d5426-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="d5426-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTigerText Messenger Secure (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5426-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5426-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d5426-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5426-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5426-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5426-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d5426-110">Prerequisites</span></span>

<span data-ttu-id="d5426-111">tooconfigure integracji usługi Azure AD z TigerText Secure Messenger należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d5426-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="d5426-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5426-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5426-113">TigerText Secure Messenger logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d5426-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5426-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d5426-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5426-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d5426-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5426-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d5426-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5426-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5426-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5426-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d5426-118">Scenario description</span></span>
<span data-ttu-id="d5426-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d5426-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5426-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d5426-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5426-121">Dodaj TigerText Secure Messenger z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d5426-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="d5426-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d5426-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="d5426-123">Dodaj TigerText Secure Messenger z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d5426-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="d5426-124">tooconfigure hello integracji programu TigerText Secure Messenger do usługi Azure AD, należy tooadd TigerText Secure Messenger z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d5426-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5426-125">**tooadd TigerText Secure Messenger z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d5426-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5426-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d5426-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d5426-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d5426-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5426-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d5426-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d5426-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5426-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d5426-133">W hello wyszukiwania wpisz **TigerText Secure Messenger**, wybierz pozycję **TigerText Secure Messenger** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5426-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Dodaj z galerii](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d5426-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d5426-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d5426-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TigerText Messenger zabezpieczenia oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d5426-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5426-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello użytkownika odpowiednik w programie TigerText Secure Messenger jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5426-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="d5426-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w programie TigerText Secure Messenger musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d5426-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="d5426-139">W programie Messenger Secure TigerText, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d5426-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5426-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TigerText Secure Messenger, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d5426-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5426-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d5426-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5426-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d5426-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5426-143">**[Tworzenie użytkownika testowego TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)**  -toohave odpowiednikiem Simona Britta Secure Messenger TigerText, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d5426-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5426-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5426-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5426-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d5426-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d5426-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d5426-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d5426-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="d5426-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="d5426-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TigerText Secure Messenger wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d5426-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5426-149">W portalu Azure na powitania hello **TigerText Secure Messenger** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d5426-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d5426-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5426-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="d5426-153">Na powitania **TigerText Secure Messenger domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d5426-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Sekcja TigerText Secure Messenger domeny i adresy URL](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="d5426-155">a.</span><span class="sxs-lookup"><span data-stu-id="d5426-155">a.</span></span> <span data-ttu-id="d5426-156">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL jako:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="d5426-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="d5426-157">b.</span><span class="sxs-lookup"><span data-stu-id="d5426-157">b.</span></span> <span data-ttu-id="d5426-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="d5426-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5426-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d5426-159">This value is not real.</span></span> <span data-ttu-id="d5426-160">Zaktualizuj tę wartość z hello rzeczywisty identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d5426-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="d5426-161">Skontaktuj się z [zespołem pomocy technicznej kliencie Secure TigerText](mailTo:prosupport@tigertext.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d5426-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="d5426-162">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d5426-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="d5426-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d5426-164">Click **Save** button.</span></span>

    ![Przycisk Zapisz](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5426-166">tooget rejestracji jednokrotnej skonfigurowana dla aplikacji, skontaktuj się z [zespołem pomocy technicznej TigerText Secure Messenger](mailTo:prosupport@tigertext.com) i podaj hello **metadanych pobrane**.</span><span class="sxs-lookup"><span data-stu-id="d5426-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="d5426-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d5426-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5426-168">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d5426-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5426-169">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5426-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d5426-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5426-170">Create an Azure AD test user</span></span>
<span data-ttu-id="d5426-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d5426-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d5426-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d5426-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5426-174">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d5426-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5426-176">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d5426-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5426-178">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5426-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Dodawanie przycisku](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5426-180">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d5426-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5426-182">a.</span><span class="sxs-lookup"><span data-stu-id="d5426-182">a.</span></span> <span data-ttu-id="d5426-183">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5426-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5426-184">b.</span><span class="sxs-lookup"><span data-stu-id="d5426-184">b.</span></span> <span data-ttu-id="d5426-185">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5426-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5426-186">c.</span><span class="sxs-lookup"><span data-stu-id="d5426-186">c.</span></span> <span data-ttu-id="d5426-187">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d5426-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5426-188">d.</span><span class="sxs-lookup"><span data-stu-id="d5426-188">d.</span></span> <span data-ttu-id="d5426-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d5426-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="d5426-190">Tworzenie użytkownika testowego TigerText zabezpieczenia w programie Messenger</span><span class="sxs-lookup"><span data-stu-id="d5426-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="d5426-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w TigerText.</span><span class="sxs-lookup"><span data-stu-id="d5426-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="d5426-192">Sprawdź dotrzeć zbyt[zespołem pomocy technicznej kliencie Secure TigerText](mailTo:prosupport@tigertext.com) użytkowników hello tooadd hello TigerText platformy.</span><span class="sxs-lookup"><span data-stu-id="d5426-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d5426-193">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5426-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d5426-194">W tej sekcji, Włącz toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="d5426-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d5426-196">**tooassign tooTigerText Simona Britta Secure Messenger, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d5426-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5426-197">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d5426-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d5426-199">Z listy aplikacji hello wybierz **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="d5426-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger listy aplikacji](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="d5426-201">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d5426-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d5426-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d5426-203">Click **Add** button.</span></span> <span data-ttu-id="d5426-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5426-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d5426-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d5426-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5426-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5426-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5426-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5426-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d5426-209">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d5426-209">Test single sign-on</span></span>

<span data-ttu-id="d5426-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d5426-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5426-211">Po kliknięciu kafelka TigerText hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TigerText aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5426-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="d5426-212">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5426-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5426-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d5426-213">Additional resources</span></span>

* [<span data-ttu-id="d5426-214">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5426-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5426-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d5426-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

