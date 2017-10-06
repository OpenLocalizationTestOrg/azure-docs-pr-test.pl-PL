---
title: 'Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="b56e9-103">Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56e9-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="b56e9-104">Z tego samouczka, dowiesz się, jak toointegrate Thoughtworks Mingle w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b56e9-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b56e9-105">Integrowanie Thoughtworks Mingle z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b56e9-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b56e9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56e9-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="b56e9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooThoughtworks Mingle (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56e9-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b56e9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b56e9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b56e9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b56e9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b56e9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b56e9-110">Prerequisites</span></span>

<span data-ttu-id="b56e9-111">tooconfigure integracji usługi Azure AD z Thoughtworks Mingle należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b56e9-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="b56e9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b56e9-113">Thoughtworks Mingle logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b56e9-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b56e9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b56e9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b56e9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b56e9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b56e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b56e9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b56e9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b56e9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b56e9-118">Scenario description</span></span>
<span data-ttu-id="b56e9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b56e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b56e9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b56e9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b56e9-121">Dodawanie Thoughtworks Mingle z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b56e9-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="b56e9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b56e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="b56e9-123">Dodawanie Thoughtworks Mingle z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b56e9-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="b56e9-124">tooconfigure hello integracji Thoughtworks Mingle do usługi Azure AD, należy tooadd Thoughtworks Mingle z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b56e9-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b56e9-125">**tooadd Thoughtworks Mingle z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b56e9-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56e9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b56e9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="b56e9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b56e9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="b56e9-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="b56e9-133">W polu wyszukiwania hello wpisz **Thoughtworks Mingle**, wybierz pozycję **Thoughtworks Mingle** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b56e9-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Thoughtworks Mingle hello listy wyników](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b56e9-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b56e9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b56e9-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b56e9-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Thoughtworks Mingle jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b56e9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="b56e9-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Thoughtworks Mingle musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b56e9-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="b56e9-139">W Thoughtworks Mingle, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b56e9-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b56e9-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b56e9-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b56e9-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b56e9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b56e9-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b56e9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b56e9-143">**[Tworzenie użytkownika testowego Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave odpowiednikiem Simona Britta w Thoughtworks Mingle, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b56e9-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b56e9-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b56e9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b56e9-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b56e9-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b56e9-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b56e9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b56e9-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b56e9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="b56e9-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b56e9-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56e9-149">W portalu Azure na powitania hello **Thoughtworks Mingle** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b56e9-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b56e9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="b56e9-153">Na powitania **Thoughtworks Mingle domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b56e9-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Mingle Thoughtworks pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="b56e9-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="b56e9-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b56e9-156">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b56e9-156">hello value is not real.</span></span> <span data-ttu-id="b56e9-157">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b56e9-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b56e9-158">Skontaktuj się z [zespołem pomocy technicznej klienta Mingle Thoughtworks](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="b56e9-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="b56e9-159">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b56e9-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="b56e9-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b56e9-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b56e9-163">Zaloguj się za tooyour **Thoughtworks Mingle** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b56e9-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="b56e9-164">Kliknij przycisk hello **Admin** , a następnie kliknij **konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="b56e9-165">![Karta Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="b56e9-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="b56e9-166">W hello **konfiguracji logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b56e9-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b56e9-167">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="b56e9-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="b56e9-168">a.</span><span class="sxs-lookup"><span data-stu-id="b56e9-168">a.</span></span> <span data-ttu-id="b56e9-169">Plik metadanych hello tooupload, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="b56e9-170">b.</span><span class="sxs-lookup"><span data-stu-id="b56e9-170">b.</span></span> <span data-ttu-id="b56e9-171">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b56e9-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b56e9-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b56e9-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b56e9-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b56e9-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b56e9-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b56e9-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56e9-175">Create an Azure AD test user</span></span>
<span data-ttu-id="b56e9-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b56e9-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="b56e9-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b56e9-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56e9-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b56e9-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b56e9-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b56e9-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b56e9-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b56e9-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b56e9-187">a.</span><span class="sxs-lookup"><span data-stu-id="b56e9-187">a.</span></span> <span data-ttu-id="b56e9-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b56e9-189">b.</span><span class="sxs-lookup"><span data-stu-id="b56e9-189">b.</span></span> <span data-ttu-id="b56e9-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b56e9-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b56e9-191">c.</span><span class="sxs-lookup"><span data-stu-id="b56e9-191">c.</span></span> <span data-ttu-id="b56e9-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b56e9-193">d.</span><span class="sxs-lookup"><span data-stu-id="b56e9-193">d.</span></span> <span data-ttu-id="b56e9-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="b56e9-195">Tworzenie użytkownika testowego Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56e9-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="b56e9-196">Dla usługi Azure AD użytkownicy toobe stanie toosign w muszą być elastycznie toohello Thoughtworks Mingle aplikacji przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b56e9-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="b56e9-197">W przypadku hello Thoughtworks Mingle Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b56e9-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="b56e9-198">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b56e9-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56e9-199">Zaloguj się za tooyour Thoughtworks Mingle witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b56e9-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="b56e9-200">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="b56e9-201">![Pierwszy projekt](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "pierwszego projektu")</span><span class="sxs-lookup"><span data-stu-id="b56e9-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="b56e9-202">Kliknij przycisk hello **Admin** , a następnie kliknij pozycję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="b56e9-203">![Użytkownicy](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="b56e9-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="b56e9-204">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-204">Click **New User**.</span></span>
   
    <span data-ttu-id="b56e9-205">![Nowy użytkownik](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="b56e9-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="b56e9-206">Na powitania **nowego użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b56e9-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b56e9-207">![Okno dialogowe nowego użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="b56e9-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="b56e9-208">a.</span><span class="sxs-lookup"><span data-stu-id="b56e9-208">a.</span></span> <span data-ttu-id="b56e9-209">Hello typu **nazwy logowania**, **Nazwa wyświetlana**, **hasła wybierz**, **Potwierdź hasło** prawidłowy Azure AD konta tooprovision do hello związanych z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="b56e9-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="b56e9-210">b.</span><span class="sxs-lookup"><span data-stu-id="b56e9-210">b.</span></span> <span data-ttu-id="b56e9-211">Jako **typ użytkownika**, wybierz pozycję **pełnej**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="b56e9-212">c.</span><span class="sxs-lookup"><span data-stu-id="b56e9-212">c.</span></span> <span data-ttu-id="b56e9-213">Kliknij przycisk **utworzyć ten profil**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="b56e9-214">Możesz użyć innych Thoughtworks Mingle użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Thoughtworks Mingle tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="b56e9-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b56e9-215">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56e9-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b56e9-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b56e9-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="b56e9-218">**tooassign tooThoughtworks Simona Britta Mingle, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b56e9-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56e9-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b56e9-221">Z listy aplikacji hello wybierz **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![Witaj Thoughtworks Mingle łącza na liście aplikacji hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="b56e9-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b56e9-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="b56e9-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b56e9-225">Click **Add** button.</span></span> <span data-ttu-id="b56e9-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="b56e9-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b56e9-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b56e9-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b56e9-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b56e9-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b56e9-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b56e9-231">Test single sign-on</span></span>

<span data-ttu-id="b56e9-232">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b56e9-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b56e9-233">Po kliknięciu kafelka Thoughtworks Mingle hello w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Thoughtworks Mingle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b56e9-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b56e9-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b56e9-234">Additional resources</span></span>

* [<span data-ttu-id="b56e9-235">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b56e9-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b56e9-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b56e9-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

