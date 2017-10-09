---
title: 'Samouczek: Integracji Azure Active Directory z Lucidchart | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="f22ca-103">Samouczek: Integracji Azure Active Directory z Lucidchart</span><span class="sxs-lookup"><span data-stu-id="f22ca-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="f22ca-104">Z tego samouczka, dowiesz się, jak toointegrate Lucidchart w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f22ca-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f22ca-105">Integracja z usługą Azure AD Lucidchart zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f22ca-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f22ca-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="f22ca-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="f22ca-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLucidchart (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f22ca-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f22ca-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f22ca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f22ca-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f22ca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f22ca-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f22ca-110">Prerequisites</span></span>

<span data-ttu-id="f22ca-111">tooconfigure integracji z usługą Azure AD z Lucidchart należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f22ca-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="f22ca-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f22ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f22ca-113">Lucidchart logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f22ca-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f22ca-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f22ca-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f22ca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f22ca-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f22ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f22ca-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f22ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f22ca-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f22ca-118">Scenario description</span></span>
<span data-ttu-id="f22ca-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f22ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f22ca-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f22ca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f22ca-121">Dodawanie Lucidchart z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f22ca-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="f22ca-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f22ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="f22ca-123">Dodawanie Lucidchart z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f22ca-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="f22ca-124">tooconfigure hello integracji Lucidchart do usługi Azure AD, należy tooadd Lucidchart z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f22ca-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f22ca-125">**tooadd Lucidchart z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f22ca-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f22ca-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f22ca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f22ca-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f22ca-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f22ca-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f22ca-133">W polu wyszukiwania hello wpisz **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-133">In hello search box, type **Lucidchart**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="f22ca-135">W panelu wyników hello zaznacz **Lucidchart**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f22ca-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f22ca-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f22ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f22ca-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lucidchart w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f22ca-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Lucidchart jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f22ca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="f22ca-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Lucidchart musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f22ca-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="f22ca-141">W Lucidchart, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="f22ca-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f22ca-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Lucidchart, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f22ca-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f22ca-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f22ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f22ca-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f22ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f22ca-145">**[Tworzenie użytkownika testowego Lucidchart](#creating-a-lucidchart-test-user)**  -toohave odpowiednikiem Simona Britta w Lucidchart, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f22ca-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f22ca-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f22ca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f22ca-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f22ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f22ca-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f22ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f22ca-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="f22ca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="f22ca-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Lucidchart, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f22ca-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f22ca-151">W portalu Azure na powitania hello **Lucidchart** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f22ca-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f22ca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="f22ca-155">Na powitania **Lucidchart domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f22ca-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="f22ca-157">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="f22ca-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="f22ca-158">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f22ca-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="f22ca-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f22ca-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f22ca-162">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Lucidchart jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f22ca-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="f22ca-163">W menu hello na górze hello, kliknij przycisk **zespołu**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="f22ca-164">![Zespół](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "zespołu")</span><span class="sxs-lookup"><span data-stu-id="f22ca-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="f22ca-165">Kliknij przycisk **aplikacji \> Zarządzanie SAML**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="f22ca-166">![Zarządzanie SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Zarządzanie SAML")</span><span class="sxs-lookup"><span data-stu-id="f22ca-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="f22ca-167">Na powitania **ustawienia uwierzytelniania SAML** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f22ca-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f22ca-168">a.</span><span class="sxs-lookup"><span data-stu-id="f22ca-168">a.</span></span> <span data-ttu-id="f22ca-169">Wybierz **Włącz uwierzytelnianie SAML**, a następnie kliknij przycisk **opcjonalnie**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="f22ca-170">![Ustawienia uwierzytelniania SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML ustawienia uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="f22ca-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="f22ca-171">b.</span><span class="sxs-lookup"><span data-stu-id="f22ca-171">b.</span></span> <span data-ttu-id="f22ca-172">W hello **domeny** tekstowym, wpisz domenę, a następnie kliknij przycisk **zmiana certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="f22ca-173">![Zmienianie certyfikatu](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Zmienianie certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="f22ca-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="f22ca-174">c.</span><span class="sxs-lookup"><span data-stu-id="f22ca-174">c.</span></span> <span data-ttu-id="f22ca-175">Otwórz z pliku metadanych pobranych, hello kopiowania zawartości, a następnie wklej go do hello **przekazać metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="f22ca-176">![Przekaż metadanych](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "przekazać metadanych")</span><span class="sxs-lookup"><span data-stu-id="f22ca-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="f22ca-177">d.</span><span class="sxs-lookup"><span data-stu-id="f22ca-177">d.</span></span> <span data-ttu-id="f22ca-178">Wybierz **automatyczne dodawanie nowych użytkowników toohello zespołu**, a następnie kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="f22ca-179">![Zapisz zmiany](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "zapisać zmiany")</span><span class="sxs-lookup"><span data-stu-id="f22ca-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="f22ca-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="f22ca-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f22ca-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="f22ca-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f22ca-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f22ca-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f22ca-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f22ca-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f22ca-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="f22ca-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f22ca-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f22ca-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f22ca-187">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f22ca-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f22ca-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f22ca-191">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f22ca-193">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f22ca-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f22ca-195">a.</span><span class="sxs-lookup"><span data-stu-id="f22ca-195">a.</span></span> <span data-ttu-id="f22ca-196">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f22ca-197">b.</span><span class="sxs-lookup"><span data-stu-id="f22ca-197">b.</span></span> <span data-ttu-id="f22ca-198">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f22ca-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f22ca-199">c.</span><span class="sxs-lookup"><span data-stu-id="f22ca-199">c.</span></span> <span data-ttu-id="f22ca-200">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f22ca-201">d.</span><span class="sxs-lookup"><span data-stu-id="f22ca-201">d.</span></span> <span data-ttu-id="f22ca-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="f22ca-203">Tworzenie użytkownika testowego Lucidchart</span><span class="sxs-lookup"><span data-stu-id="f22ca-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="f22ca-204">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="f22ca-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="f22ca-205">Gdy przypisany użytkownik podejmie próbę toolog do Lucidchart za pomocą panelu dostępu hello, Lucidchart sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f22ca-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="f22ca-206">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="f22ca-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f22ca-207">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f22ca-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f22ca-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="f22ca-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f22ca-210">**tooassign tooLucidchart Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f22ca-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f22ca-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f22ca-213">Z listy aplikacji hello wybierz **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="f22ca-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f22ca-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f22ca-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f22ca-217">Click **Add** button.</span></span> <span data-ttu-id="f22ca-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f22ca-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f22ca-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f22ca-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f22ca-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f22ca-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f22ca-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f22ca-223">Testing single sign-on</span></span>

<span data-ttu-id="f22ca-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f22ca-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f22ca-225">Po kliknięciu kafelka Lucidchart hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Lucidchart aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f22ca-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="f22ca-226">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f22ca-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f22ca-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f22ca-227">Additional resources</span></span>

* [<span data-ttu-id="f22ca-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f22ca-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f22ca-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f22ca-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

