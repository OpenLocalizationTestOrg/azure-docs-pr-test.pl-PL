---
title: 'Samouczek: Integracji Azure Active Directory z @Task| Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="17c63-103">Samouczek: Integracji Azure Active Directory z@Task</span><span class="sxs-lookup"><span data-stu-id="17c63-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="17c63-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate @Task z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17c63-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="17c63-105">Integrowanie @Task z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="17c63-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="17c63-106">Można kontrolować w usłudze Azure AD, który ma dostęptoo@Task</span><span class="sxs-lookup"><span data-stu-id="17c63-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="17c63-107">Umożliwia użytkownikom uzyskać tooautomatically zalogowane too@Task (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c63-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="17c63-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="17c63-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="17c63-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17c63-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17c63-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17c63-110">Prerequisites</span></span>
<span data-ttu-id="17c63-111">Integracja tooconfigure usługi Azure AD z @Task, potrzebujesz hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="17c63-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="17c63-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c63-112">An Azure AD subscription</span></span>
* <span data-ttu-id="17c63-113">@Task Jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="17c63-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17c63-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="17c63-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="17c63-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="17c63-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="17c63-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="17c63-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="17c63-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17c63-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="17c63-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="17c63-118">Scenario Description</span></span>
<span data-ttu-id="17c63-119">Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="17c63-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="17c63-120">Scenariusz Hello opisane w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="17c63-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="17c63-121">Dodawanie @Task z galerii hello</span><span class="sxs-lookup"><span data-stu-id="17c63-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="17c63-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="17c63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="17c63-123">Dodawanie @Task z galerii hello</span><span class="sxs-lookup"><span data-stu-id="17c63-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="17c63-124">Integracja hello tooconfigure @Task do usługi Azure AD, należy tooadd @Task z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="17c63-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17c63-125">**tooadd @Task z galerii hello wykonywać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="17c63-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c63-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17c63-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1] 
2. <span data-ttu-id="17c63-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="17c63-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="17c63-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="17c63-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2] 
4. <span data-ttu-id="17c63-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="17c63-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3] 
5. <span data-ttu-id="17c63-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="17c63-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4] 
6. <span data-ttu-id="17c63-135">W polu wyszukiwania hello wpisz  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="17c63-135">In hello search box, type **@Task**.</span></span>
   
    ![Aplikacje][5] 
7. <span data-ttu-id="17c63-137">Wybierz w okienku wyników hello  **@Task** , a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="17c63-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplikacje][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17c63-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="17c63-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17c63-140">Witaj celem tej sekcji jest tooshow należy jak pojedynczy tooconfigure i testowych usługi Azure AD logowania z @Task w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="17c63-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17c63-141">Dla pojedynczego logowania jednokrotnego toowork, usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w @Task jest tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17c63-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="17c63-142">Innymi słowy, relacja linku między użytkownika usługi Azure AD i hello użytkownikowi w @Task musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="17c63-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="17c63-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w @Task.</span><span class="sxs-lookup"><span data-stu-id="17c63-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="17c63-144">tooconfigure i testowych usługi Azure AD logowanie jednokrotne z @Task, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="17c63-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17c63-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="17c63-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17c63-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17c63-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17c63-147">**[Tworzenie @Tasktest użytkownika](#creating-a-halogen-software-test-user)**  -toohave a odpowiednikiem Simona Britta w @Taskthat jej reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17c63-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="17c63-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="17c63-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17c63-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="17c63-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17c63-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17c63-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="17c63-151">Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w sieci @Task aplikacji.</span><span class="sxs-lookup"><span data-stu-id="17c63-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="17c63-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z @Task, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="17c63-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c63-153">W hello klasycznego portalu Azure na powitania  **@Task**  strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="17c63-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="17c63-155">Na powitania **jak ma toosign użytkowników na too@Task**  wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][7] 
3. <span data-ttu-id="17c63-157">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17c63-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Konfiguruj ustawienia aplikacji][8] 
   
     <span data-ttu-id="17c63-159">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-159">a.</span></span> <span data-ttu-id="17c63-160">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używane przez użytkowników z toosign na tooyour @Task aplikacji (np.:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="17c63-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="17c63-161">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-161">b.</span></span> <span data-ttu-id="17c63-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-162">Click **Next**.</span></span>
4. <span data-ttu-id="17c63-163">Na powitania **skonfigurować logowanie jednokrotne w @Task**  kliknij przycisk **pobierania metadanych**, Zapisz plik metadanych hello lokalnie na komputerze, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Co to jest program Azure AD Connect][9] 
5. <span data-ttu-id="17c63-165">Logowania jednokrotnego tooyour @Task witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="17c63-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="17c63-166">Przejdź za**pojedynczy znak w konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="17c63-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="17c63-167">Na powitania **rejestracji jednokrotnej** okna dialogowego, wykonaj następujące kroki hello</span><span class="sxs-lookup"><span data-stu-id="17c63-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][23]
   
    <span data-ttu-id="17c63-169">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-169">a.</span></span> <span data-ttu-id="17c63-170">Jako **typu**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="17c63-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="17c63-171">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-171">b.</span></span> <span data-ttu-id="17c63-172">Wybierz **usługi identyfikator dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="17c63-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="17c63-173">c.</span><span class="sxs-lookup"><span data-stu-id="17c63-173">c.</span></span> <span data-ttu-id="17c63-174">Na powitania klasycznego portalu Azure, skopiuj hello **zdalnego adresu URL logowania**i wklej go do hello **adresu URL logowania do portalu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="17c63-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="17c63-175">d.</span><span class="sxs-lookup"><span data-stu-id="17c63-175">d.</span></span> <span data-ttu-id="17c63-176">Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy adres URL usługi Sign-Out**, a następnie wklej go do hello **Sign-Out URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="17c63-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="17c63-177">e.</span><span class="sxs-lookup"><span data-stu-id="17c63-177">e.</span></span> <span data-ttu-id="17c63-178">Hello klasycznego portalu Azure, skopiuj hello **Zmień adres URL hasła**, a następnie wklej go do hello **Zmień adres URL hasła** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="17c63-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="17c63-179">f.</span><span class="sxs-lookup"><span data-stu-id="17c63-179">f.</span></span> <span data-ttu-id="17c63-180">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="17c63-180">Click **Save**.</span></span>
8. <span data-ttu-id="17c63-181">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Co to jest program Azure AD Connect][10]
9. <span data-ttu-id="17c63-183">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="17c63-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Co to jest program Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17c63-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c63-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="17c63-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17c63-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="17c63-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="17c63-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c63-189">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17c63-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="17c63-191">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="17c63-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="17c63-192">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="17c63-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="17c63-194">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="17c63-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="17c63-196">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17c63-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="17c63-198">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-198">a.</span></span> <span data-ttu-id="17c63-199">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="17c63-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="17c63-200">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-200">b.</span></span> <span data-ttu-id="17c63-201">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17c63-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="17c63-202">c.</span><span class="sxs-lookup"><span data-stu-id="17c63-202">c.</span></span> <span data-ttu-id="17c63-203">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-203">Click **Next**.</span></span>
6. <span data-ttu-id="17c63-204">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17c63-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="17c63-206">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-206">a.</span></span> <span data-ttu-id="17c63-207">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="17c63-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="17c63-208">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-208">b.</span></span> <span data-ttu-id="17c63-209">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="17c63-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="17c63-210">c.</span><span class="sxs-lookup"><span data-stu-id="17c63-210">c.</span></span> <span data-ttu-id="17c63-211">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="17c63-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="17c63-212">d.</span><span class="sxs-lookup"><span data-stu-id="17c63-212">d.</span></span> <span data-ttu-id="17c63-213">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="17c63-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="17c63-214">e.</span><span class="sxs-lookup"><span data-stu-id="17c63-214">e.</span></span> <span data-ttu-id="17c63-215">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="17c63-215">Click **Next**.</span></span>

7. <span data-ttu-id="17c63-216">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="17c63-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="17c63-218">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17c63-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="17c63-220">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-220">a.</span></span> <span data-ttu-id="17c63-221">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="17c63-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="17c63-222">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-222">b.</span></span> <span data-ttu-id="17c63-223">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="17c63-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="17c63-224">Tworzenie @Task użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="17c63-224">Creating an @Task test user</span></span>
<span data-ttu-id="17c63-225">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w @Task.</span><span class="sxs-lookup"><span data-stu-id="17c63-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="17c63-226">**toocreate użytkownika o nazwie Simona Britta w @Task, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="17c63-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c63-227">Zaloguj się na tooyour @Task witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="17c63-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="17c63-228">W menu hello na górze hello, kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="17c63-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="17c63-229">Kliknij przycisk **nowej osoby**.</span><span class="sxs-lookup"><span data-stu-id="17c63-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="17c63-230">W oknie dialogowym nowej osoby hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="17c63-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Utwórz @Task użytkownika testowego][21] 
   
    <span data-ttu-id="17c63-232">a.</span><span class="sxs-lookup"><span data-stu-id="17c63-232">a.</span></span> <span data-ttu-id="17c63-233">W hello **imię** tekstowym, wpisz "Britta".</span><span class="sxs-lookup"><span data-stu-id="17c63-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="17c63-234">b.</span><span class="sxs-lookup"><span data-stu-id="17c63-234">b.</span></span> <span data-ttu-id="17c63-235">W hello **nazwisko** tekstowym, wpisz "Simona".</span><span class="sxs-lookup"><span data-stu-id="17c63-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="17c63-236">c.</span><span class="sxs-lookup"><span data-stu-id="17c63-236">c.</span></span> <span data-ttu-id="17c63-237">W hello **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="17c63-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="17c63-238">d.</span><span class="sxs-lookup"><span data-stu-id="17c63-238">d.</span></span> <span data-ttu-id="17c63-239">Kliknij przycisk **Dodaj osobę**.</span><span class="sxs-lookup"><span data-stu-id="17c63-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17c63-240">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17c63-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="17c63-241">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej przez udostępnienie jej too@Task.</span><span class="sxs-lookup"><span data-stu-id="17c63-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="17c63-243">**tooassign Simona Britta too@Task, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="17c63-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="17c63-244">Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="17c63-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][201] 
2. <span data-ttu-id="17c63-246">Z listy aplikacji hello wybierz  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="17c63-246">In hello applications list, select **@Task**.</span></span>
   
    ![Przypisz użytkownika][202] 
3. <span data-ttu-id="17c63-248">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="17c63-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 
4. <span data-ttu-id="17c63-250">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="17c63-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="17c63-251">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="17c63-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="17c63-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17c63-253">Testing Single Sign-On</span></span>
<span data-ttu-id="17c63-254">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="17c63-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="17c63-255">Po kliknięciu hello @Task kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour @Task aplikacji.</span><span class="sxs-lookup"><span data-stu-id="17c63-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17c63-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="17c63-256">Additional Resources</span></span>
* [<span data-ttu-id="17c63-257">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17c63-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17c63-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17c63-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






