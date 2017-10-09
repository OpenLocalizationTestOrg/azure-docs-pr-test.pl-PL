---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="7ae5e-103">Samouczek: Integracji Azure Active Directory z Dropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="7ae5e-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="7ae5e-104">Z tego samouczka, dowiesz się, jak toointegrate Dropbox dla firm z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ae5e-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ae5e-105">Integrowanie usługi Dropbox dla firm z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ae5e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="7ae5e-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="7ae5e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDropbox dla firm (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ae5e-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ae5e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7ae5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ae5e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ae5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ae5e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7ae5e-110">Prerequisites</span></span>

<span data-ttu-id="7ae5e-111">tooconfigure integracji usługi Azure AD z Dropbox dla firm, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="7ae5e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ae5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ae5e-113">Dropbox dla firm logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7ae5e-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ae5e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ae5e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ae5e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ae5e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ae5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ae5e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7ae5e-118">Scenario description</span></span>
<span data-ttu-id="7ae5e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ae5e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ae5e-121">Dodawanie skrzynki dla firm z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7ae5e-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="7ae5e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7ae5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="7ae5e-123">Dodawanie skrzynki dla firm z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7ae5e-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="7ae5e-124">integracji hello tooconfigure Dropbox dla firm z usługą Azure AD, należy tooadd Dropbox dla firm z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ae5e-125">**tooadd Dropbox dla firm z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7ae5e-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ae5e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7ae5e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ae5e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7ae5e-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7ae5e-133">W polu wyszukiwania hello wpisz **Dropbox dla firm**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="7ae5e-135">W panelu wyników hello, wybierz **Dropbox dla firm**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ae5e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7ae5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ae5e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7ae5e-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ae5e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow w Dropbox dla firm użytkownika odpowiednikiem hello jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="7ae5e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Dropbox dla firm musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="7ae5e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="7ae5e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ae5e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ae5e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ae5e-145">**[Tworzenie skrzynki dla użytkownika testowego firm](#creating-a-dropbox-for-business-test-user)**  -toohave odpowiednikiem Simona Britta w Dropbox dla firm, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ae5e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ae5e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ae5e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7ae5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ae5e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowania jednokrotnego w usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="7ae5e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7ae5e-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ae5e-151">W portalu Azure na powitania hello **Dropbox dla firm** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7ae5e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="7ae5e-155">Na powitania **Dropbox domeny biznesowych i adresów URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="7ae5e-156">a.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-156">a.</span></span> <span data-ttu-id="7ae5e-157">Zaloguj się na tooyour Dropbox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="7ae5e-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="7ae5e-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7ae5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-159">b.</span></span> <span data-ttu-id="7ae5e-160">W okienku nawigacji hello po lewej stronie powitania kliknij **konsoli administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="7ae5e-161">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="7ae5e-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7ae5e-162">c.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-162">c.</span></span> <span data-ttu-id="7ae5e-163">Na powitania **konsoli administracyjnej**, kliknij przycisk **uwierzytelniania** w okienku nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="7ae5e-164">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="7ae5e-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7ae5e-165">d.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-165">d.</span></span> <span data-ttu-id="7ae5e-166">W hello **logowanie jednokrotne** zaznacz **Włącz rejestrację jednokrotną**, a następnie kliknij przycisk **więcej** tooexpand w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="7ae5e-167">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="7ae5e-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7ae5e-168">e.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-168">e.</span></span> <span data-ttu-id="7ae5e-169">Skopiuj adres URL hello obok zbyt**użytkownicy mogą rejestrować wprowadź swój adres e-mail lub można przejść bezpośrednio do**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="7ae5e-171">f.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-171">f.</span></span> <span data-ttu-id="7ae5e-172">W portalu Azure w hello hello **adres URL logowania** pole tekstowe, wklej adres URL z hello.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="7ae5e-174">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="7ae5e-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ae5e-175">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-175">This value is not real value.</span></span> <span data-ttu-id="7ae5e-176">Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania otrzymasz od jednej sekcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="7ae5e-177">Skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta Business](https://www.dropbox.com/business/contact) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="7ae5e-178">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="7ae5e-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-180">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ae5e-182">Na powitania **Dropbox konfiguracji Business** , kliknij przycisk **Konfigurowanie skrzynki dla firm** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ae5e-183">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7ae5e-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="7ae5e-185">tooconfigure rejestracji jednokrotnej w **Dropbox dla firm** po stronie znajduje się w usłudze Dropbox dla dzierżawy biznesowych, w hello **logowanie jednokrotne** sekcji hello **uwierzytelniania** strony, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="7ae5e-186">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="7ae5e-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7ae5e-187">a.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-187">a.</span></span> <span data-ttu-id="7ae5e-188">Kliknij przycisk **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-188">Click **Required**.</span></span>
   
    <span data-ttu-id="7ae5e-189">b.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-189">b.</span></span> <span data-ttu-id="7ae5e-190">W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="7ae5e-191">c.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-191">c.</span></span> <span data-ttu-id="7ae5e-192">Kliknij przycisk **wybierz certyfikat**, a następnie przejdź tooyour **pliku zakodowanego certyfikatu Base64**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="7ae5e-193">d.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-193">d.</span></span> <span data-ttu-id="7ae5e-194">Kliknij przycisk **zapisać zmiany** toocomplete hello konfiguracji w usłudze DropBox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="7ae5e-195">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="7ae5e-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ae5e-196">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ae5e-197">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ae5e-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ae5e-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ae5e-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ae5e-199">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7ae5e-201">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7ae5e-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ae5e-202">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="7ae5e-204">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ae5e-206">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ae5e-208">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7ae5e-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ae5e-210">a.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-210">a.</span></span> <span data-ttu-id="7ae5e-211">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ae5e-212">b.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-212">b.</span></span> <span data-ttu-id="7ae5e-213">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ae5e-214">c.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-214">c.</span></span> <span data-ttu-id="7ae5e-215">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ae5e-216">d.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-216">d.</span></span> <span data-ttu-id="7ae5e-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="7ae5e-218">Tworzenie skrzynki dla firm użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="7ae5e-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="7ae5e-219">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="7ae5e-220">Dropbox dla firm obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="7ae5e-221">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-221">There is no action item for you in this section.</span></span> <span data-ttu-id="7ae5e-222">Jeśli użytkownik nie istnieje w Dropbox dla firm, nowy jest tworzony podczas próby tooaccess Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="7ae5e-223">Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta biznesowa](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="7ae5e-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7ae5e-224">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ae5e-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7ae5e-225">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7ae5e-227">**tooassign tooDropbox Simona Britta dla firm, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7ae5e-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ae5e-228">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7ae5e-230">Z listy aplikacji hello wybierz **Dropbox dla firm**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="7ae5e-232">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7ae5e-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-234">Click **Add** button.</span></span> <span data-ttu-id="7ae5e-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7ae5e-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ae5e-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ae5e-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ae5e-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7ae5e-240">Testing single sign-on</span></span>

<span data-ttu-id="7ae5e-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ae5e-242">Po kliknięciu hello skrzynki dla firm kafelka w hello Panel dostępu, należy pobrać strony logowania o usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="7ae5e-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ae5e-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7ae5e-243">Additional resources</span></span>

* [<span data-ttu-id="7ae5e-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ae5e-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ae5e-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ae5e-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7ae5e-246">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="7ae5e-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

