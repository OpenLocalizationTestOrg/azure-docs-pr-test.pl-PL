---
title: 'Samouczek: Integracji Azure Active Directory z Halosys | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Halosys z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="6b0f7-103">Samouczek: Integracji Azure Active Directory z Halosys</span><span class="sxs-lookup"><span data-stu-id="6b0f7-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="6b0f7-104">Z tego samouczka, dowiesz się, jak toointegrate Halosys w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b0f7-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b0f7-105">Integracja z usługą Azure AD Halosys zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b0f7-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHalosys</span><span class="sxs-lookup"><span data-stu-id="6b0f7-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="6b0f7-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHalosys (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0f7-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b0f7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b0f7-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="6b0f7-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b0f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b0f7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b0f7-110">Prerequisites</span></span>

<span data-ttu-id="6b0f7-111">tooconfigure integracji z usługą Azure AD z Halosys należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="6b0f7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b0f7-113">Halosys jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6b0f7-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="6b0f7-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="6b0f7-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b0f7-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6b0f7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b0f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="6b0f7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6b0f7-118">Scenario description</span></span>
<span data-ttu-id="6b0f7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="6b0f7-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b0f7-121">Dodawanie Halosys z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6b0f7-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="6b0f7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b0f7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="6b0f7-123">Dodawanie Halosys z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6b0f7-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="6b0f7-124">tooconfigure hello integracji Halosys do usługi Azure AD, należy tooadd Halosys z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b0f7-125">**tooadd Halosys z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b0f7-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Usługa Active Directory][1]
2. <span data-ttu-id="6b0f7-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="6b0f7-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="6b0f7-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="6b0f7-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplikacje][4]

6. <span data-ttu-id="6b0f7-135">W polu wyszukiwania hello wpisz **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-135">In hello search box, type **Halosys**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="6b0f7-137">Wybierz w okienku wyników hello **Halosys**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b0f7-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b0f7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b0f7-140">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Halosys w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b0f7-141">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Halosys jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="6b0f7-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Halosys musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="6b0f7-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Halosys.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="6b0f7-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Halosys, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b0f7-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b0f7-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b0f7-147">**[Tworzenie użytkownika testowego Halosys](#creating-a-halosys-test-user)**  -toohave odpowiednikiem Simona Britta w Halosys, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6b0f7-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b0f7-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b0f7-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b0f7-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b0f7-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w aplikacji Halosys.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="6b0f7-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Halosys, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b0f7-153">W klasycznym portalu hello na powitania **Halosys** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="6b0f7-155">Na powitania **jak ma toosign użytkowników na tooHalosys** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="6b0f7-157">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="6b0f7-159">a.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-159">a.</span></span> <span data-ttu-id="6b0f7-160">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używanych przez aplikację Halosys toosign na tooyour użytkowników przy użyciu hello następującego wzorca: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="6b0f7-161">Witaj b.In **adres URL identyfikatora** pole tekstowe, wprowadź adres URL hello w hello następującego wzorca: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="6b0f7-162">Na powitania **skonfigurować logowanie jednokrotne w Halosys** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="6b0f7-164">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Halosys i podaj następujący hello:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="6b0f7-165">• hello pobrane **pliku metadanych**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="6b0f7-166">• hello **adres URL logowania jednokrotnego SAML**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="6b0f7-167">W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="6b0f7-169">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD rejestracji jednokrotnej][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b0f7-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0f7-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b0f7-172">W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="6b0f7-174">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b0f7-175">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="6b0f7-177">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="6b0f7-178">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b0f7-180">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="6b0f7-182">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj następujące kroki hello: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="6b0f7-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="6b0f7-183">a.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-183">a.</span></span> <span data-ttu-id="6b0f7-184">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="6b0f7-185">b.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-185">b.</span></span> <span data-ttu-id="6b0f7-186">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b0f7-187">c.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-187">c.</span></span> <span data-ttu-id="6b0f7-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-188">Click **Next**.</span></span>

6.  <span data-ttu-id="6b0f7-189">Na powitania **profilu użytkownika** okna dialogowego wykonaj następujące kroki hello: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="6b0f7-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="6b0f7-190">a.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-190">a.</span></span> <span data-ttu-id="6b0f7-191">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="6b0f7-192">b.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-192">b.</span></span> <span data-ttu-id="6b0f7-193">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="6b0f7-194">c.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-194">c.</span></span> <span data-ttu-id="6b0f7-195">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="6b0f7-196">d.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-196">d.</span></span> <span data-ttu-id="6b0f7-197">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="6b0f7-198">e.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-198">e.</span></span> <span data-ttu-id="6b0f7-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-199">Click **Next**.</span></span>

7. <span data-ttu-id="6b0f7-200">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="6b0f7-202">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6b0f7-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="6b0f7-204">a.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-204">a.</span></span> <span data-ttu-id="6b0f7-205">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="6b0f7-206">b.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-206">b.</span></span> <span data-ttu-id="6b0f7-207">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="6b0f7-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="6b0f7-208">Tworzenie użytkownika testowego Halosys</span><span class="sxs-lookup"><span data-stu-id="6b0f7-208">Creating a Halosys test user</span></span>

<span data-ttu-id="6b0f7-209">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Halosys.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="6b0f7-210">Należy skontaktować się z Halosys pomocy technicznej zespół tooadd hello użytkowników hello Halosys platformy.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6b0f7-211">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b0f7-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6b0f7-212">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooHalosys dostępu.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6b0f7-214">**tooassign tooHalosys Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6b0f7-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b0f7-215">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6b0f7-217">Z listy aplikacji hello wybierz **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-217">In hello applications list, select **Halosys**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="6b0f7-219">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-219">In hello menu on hello top, click **Users**.</span></span>

    ![Przypisz użytkownika][203]

4. <span data-ttu-id="6b0f7-221">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="6b0f7-222">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="6b0f7-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b0f7-224">Testing single sign-on</span></span>

<span data-ttu-id="6b0f7-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b0f7-226">Po kliknięciu powitalne Halosys kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Halosys aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b0f7-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6b0f7-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6b0f7-227">Additional resources</span></span>

* [<span data-ttu-id="6b0f7-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b0f7-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b0f7-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b0f7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
