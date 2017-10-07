---
title: 'Samouczek: Integracji Azure Active Directory z NetDocuments | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="dd4f5-103">Samouczek: Integracji Azure Active Directory z NetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd4f5-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="dd4f5-104">Z tego samouczka, dowiesz się, jak toointegrate NetDocuments w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd4f5-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd4f5-105">Integracja z usługą Azure AD NetDocuments zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd4f5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd4f5-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="dd4f5-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNetDocuments (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4f5-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd4f5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dd4f5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd4f5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd4f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd4f5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd4f5-110">Prerequisites</span></span>

<span data-ttu-id="dd4f5-111">tooconfigure integracji z usługą Azure AD z NetDocuments należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="dd4f5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd4f5-113">NetDocuments logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dd4f5-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd4f5-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd4f5-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd4f5-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd4f5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd4f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd4f5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dd4f5-118">Scenario description</span></span>
<span data-ttu-id="dd4f5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd4f5-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd4f5-121">Dodawanie NetDocuments z galerii hello</span><span class="sxs-lookup"><span data-stu-id="dd4f5-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="dd4f5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dd4f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="dd4f5-123">Dodawanie NetDocuments z galerii hello</span><span class="sxs-lookup"><span data-stu-id="dd4f5-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="dd4f5-124">tooconfigure hello integracji NetDocuments do usługi Azure AD, należy tooadd NetDocuments z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd4f5-125">**tooadd NetDocuments z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="dd4f5-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd4f5-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="dd4f5-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd4f5-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="dd4f5-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="dd4f5-133">W polu wyszukiwania hello wpisz **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-133">In hello search box, type **NetDocuments**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="dd4f5-135">W panelu wyników hello zaznacz **NetDocuments**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd4f5-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dd4f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd4f5-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z NetDocuments w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd4f5-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w NetDocuments jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="dd4f5-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w NetDocuments musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="dd4f5-141">W NetDocuments, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd4f5-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z NetDocuments, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd4f5-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd4f5-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd4f5-145">**[Tworzenie użytkownika testowego NetDocuments](#creating-a-netdocuments-test-user)**  -toohave odpowiednikiem Simona Britta w NetDocuments, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd4f5-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd4f5-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd4f5-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dd4f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd4f5-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="dd4f5-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z NetDocuments, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="dd4f5-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd4f5-151">W portalu Azure na powitania hello **NetDocuments** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="dd4f5-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="dd4f5-155">Na powitania **NetDocuments domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="dd4f5-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-157">a.</span></span> <span data-ttu-id="dd4f5-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="dd4f5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="dd4f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-159">b.</span></span> <span data-ttu-id="dd4f5-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="dd4f5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd4f5-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-161">These values are not real.</span></span> <span data-ttu-id="dd4f5-162">Witaj rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="dd4f5-163">Skontaktuj się z [NetDocuments obsługuje zespołu](https://support.netdocuments.com/hc/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="dd4f5-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="dd4f5-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd4f5-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy NetDocuments jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="dd4f5-169">Przejdź za**Admin**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="dd4f5-170">Kliknij przycisk **Dodawanie i usuwanie użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="dd4f5-171">![Repozytorium](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "repozytorium")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="dd4f5-172">Kliknij przycisk **skonfiguruj zaawansowane opcje uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="dd4f5-173">![Skonfiguruj zaawansowane opcje uwierzytelniania](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "skonfiguruj zaawansowane opcje uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="dd4f5-174">Na powitania **tożsamości federacyjnych** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd4f5-175">![Federacyjna Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "federacyjnych Identitty")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="dd4f5-176">a.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-176">a.</span></span> <span data-ttu-id="dd4f5-177">Jako **typ serwera tożsamości federacyjnych**, wybierz pozycję **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="dd4f5-178">b.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-178">b.</span></span> <span data-ttu-id="dd4f5-179">Kliknij przycisk **wybierz plik**, tooupload hello pobrany plik metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="dd4f5-180">c.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-180">c.</span></span> <span data-ttu-id="dd4f5-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="dd4f5-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="dd4f5-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd4f5-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd4f5-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd4f5-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd4f5-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4f5-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd4f5-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="dd4f5-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="dd4f5-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd4f5-189">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd4f5-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd4f5-193">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd4f5-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dd4f5-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd4f5-197">a.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-197">a.</span></span> <span data-ttu-id="dd4f5-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd4f5-199">b.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-199">b.</span></span> <span data-ttu-id="dd4f5-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd4f5-201">c.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-201">c.</span></span> <span data-ttu-id="dd4f5-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd4f5-203">d.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-203">d.</span></span> <span data-ttu-id="dd4f5-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="dd4f5-205">Tworzenie użytkownika testowego NetDocuments</span><span class="sxs-lookup"><span data-stu-id="dd4f5-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="dd4f5-206">toolog użytkowników tooenable usługi Azure AD w tooNetDocuments, muszą mieć przydzielone do NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="dd4f5-207">W przypadku hello NetDocuments Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="dd4f5-208">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dd4f5-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd4f5-209">SING na tooyour **NetDocuments** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="dd4f5-210">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="dd4f5-211">![Administrator](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="dd4f5-212">Kliknij przycisk **Dodawanie i usuwanie użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="dd4f5-213">![Repozytorium](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "repozytorium")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="dd4f5-214">W hello **adres E-mail** tekstowym, wpisz adres e-mail hello prawidłowe konto usługi Azure Active Directory tooprovision, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="dd4f5-215">![Adres e-mail](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "adres E-mail")</span><span class="sxs-lookup"><span data-stu-id="dd4f5-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dd4f5-216">Właściciel konta usługi Azure Active Directory Hello otrzyma wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="dd4f5-217">Możesz użyć innych NetDocuments użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision NetDocuments usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd4f5-218">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4f5-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd4f5-219">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNetDocuments.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="dd4f5-221">**tooassign tooNetDocuments Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dd4f5-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd4f5-222">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dd4f5-224">Z listy aplikacji hello wybierz **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="dd4f5-226">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="dd4f5-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-228">Click **Add** button.</span></span> <span data-ttu-id="dd4f5-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="dd4f5-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd4f5-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd4f5-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd4f5-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dd4f5-234">Testing single sign-on</span></span>

<span data-ttu-id="dd4f5-235">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd4f5-236">Po kliknięciu powitalne NetDocuments kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour NetDocuments aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dd4f5-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="dd4f5-237">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd4f5-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd4f5-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dd4f5-238">Additional resources</span></span>

* [<span data-ttu-id="dd4f5-239">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd4f5-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd4f5-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd4f5-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

