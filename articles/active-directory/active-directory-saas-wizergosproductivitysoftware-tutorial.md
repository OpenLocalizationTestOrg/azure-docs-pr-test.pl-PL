---
title: 'Samouczek: Integracji Azure Active Directory z Wizergos oprogramowanie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Wizergos wydajności oprogramowania."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="bdf86-103">Samouczek: Integracji Azure Active Directory z Wizergos wydajności oprogramowania</span><span class="sxs-lookup"><span data-stu-id="bdf86-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="bdf86-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate Wizergos wydajności oprogramowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdf86-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdf86-105">Integrowanie Wizergos wydajności oprogramowania z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bdf86-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="bdf86-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooWizergos oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="bdf86-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="bdf86-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWizergos oprogramowanie rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="bdf86-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bdf86-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="bdf86-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdf86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdf86-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bdf86-110">Prerequisites</span></span>
<span data-ttu-id="bdf86-111">tooconfigure integracji usługi Azure AD z oprogramowaniem wydajność Wizergos należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bdf86-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="bdf86-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-112">An Azure AD subscription</span></span>
* <span data-ttu-id="bdf86-113">Subskrypcja Wizergos wydajności oprogramowania logowanie Jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="bdf86-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="bdf86-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bdf86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="bdf86-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bdf86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bdf86-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bdf86-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bdf86-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdf86-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdf86-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bdf86-118">Scenario description</span></span>
<span data-ttu-id="bdf86-119">Celem Hello tego samouczka jest tooenable możesz tootest logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bdf86-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="bdf86-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bdf86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdf86-121">Dodawanie Wizergos oprogramowanie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bdf86-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="bdf86-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="bdf86-123">Dodawanie Wizergos oprogramowanie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bdf86-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="bdf86-124">tooconfigure hello integracji Wizergos wydajności oprogramowania do usługi Azure AD, należy tooadd Wizergos wydajności oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bdf86-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdf86-125">**tooadd Wizergos oprogramowanie z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bdf86-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdf86-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="bdf86-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="bdf86-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bdf86-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="bdf86-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="bdf86-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="bdf86-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="bdf86-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="bdf86-135">W polu wyszukiwania hello wpisz **Wizergos oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="bdf86-137">W panelu wyników hello, wybierz **Wizergos wydajności oprogramowania**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bdf86-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Wybieranie aplikacji hello w galerii hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="bdf86-139">Konfiguracja i testowanie logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="bdf86-140">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowania Azure AD z logowania jednokrotnego przy użyciu Wizergos wydajności oprogramowania na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bdf86-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdf86-141">Dla toowork logowania jednokrotnego usługi Azure AD musi tooknow jest użytkownika odpowiednikiem hello w Wizergos oprogramowanie tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="bdf86-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi Wizergos wydajności oprogramowania musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bdf86-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="bdf86-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bdf86-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="bdf86-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BynWizergos Softwareder wydajności, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bdf86-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdf86-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bdf86-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdf86-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bdf86-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdf86-147">**[Tworzenie użytkownika testowego oprogramowanie Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave odpowiednikiem Simona Britta Wizergos wydajności oprogramowania, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="bdf86-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bdf86-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdf86-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bdf86-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="bdf86-150">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="bdf86-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="bdf86-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować rejestracji jednokrotnej w aplikacji Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bdf86-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="bdf86-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Wizergos oprogramowanie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bdf86-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdf86-153">W klasycznym portalu hello na powitania **oprogramowanie Wizergos** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bdf86-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="bdf86-155">Na powitania **jak ma toosign użytkowników na tooWizergos oprogramowanie** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="bdf86-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="bdf86-157">Na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="bdf86-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="bdf86-159">Na powitania **skonfigurować logowanie jednokrotne w oprogramowanie Wizergos** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik hello na tym komputerze:</span><span class="sxs-lookup"><span data-stu-id="bdf86-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="bdf86-161">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour Wizergos oprogramowanie dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="bdf86-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="bdf86-162">Wybierz z hello hamburger menu **Admin**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="bdf86-164">Na stronie Administracja w menu po lewej stronie wybierz **uwierzytelniania** i wybierz polecenie **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="bdf86-166">Wykonaj następujące kroki powitania **uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bdf86-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="bdf86-168">Kliknij przycisk **przekazać** hello tooupload przycisk pobrać certyfikatu z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="bdf86-169">W hello **adres URL wystawcy** pole tekstowe umieścić wartość hello **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="bdf86-170">W hello **URL rejestracji jednokrotnej** pole tekstowe umieścić wartość hello **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="bdf86-171">W hello **pojedynczego adresu URL Sign-Out** pole tekstowe umieścić wartość hello **pojedynczy adres URL usługi Sign-out** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdf86-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="bdf86-172">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bdf86-172">Click **Save** button.</span></span>
9. <span data-ttu-id="bdf86-173">W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]
10. <span data-ttu-id="bdf86-175">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bdf86-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-177">Create an Azure AD test user</span></span>
<span data-ttu-id="bdf86-178">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bdf86-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="bdf86-180">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bdf86-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdf86-181">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="bdf86-183">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="bdf86-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bdf86-184">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="bdf86-186">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="bdf86-188">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bdf86-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="bdf86-190">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="bdf86-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="bdf86-191">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="bdf86-192">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-192">Click **Next**.</span></span>
6. <span data-ttu-id="bdf86-193">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bdf86-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="bdf86-195">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="bdf86-196">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="bdf86-197">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="bdf86-198">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="bdf86-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-199">Click **Next**.</span></span>
7. <span data-ttu-id="bdf86-200">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="bdf86-202">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bdf86-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="bdf86-204">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="bdf86-205">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="bdf86-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="bdf86-206">Tworzenie użytkownika testowego Wizergos wydajności oprogramowania</span><span class="sxs-lookup"><span data-stu-id="bdf86-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="bdf86-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Wizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bdf86-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="bdf86-208">Proszę współpracować z zespołem pomocy technicznej Wizergos wydajności oprogramowania za pomocą [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello użytkowników hello Wizergos wydajności oprogramowania platformy.</span><span class="sxs-lookup"><span data-stu-id="bdf86-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bdf86-209">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdf86-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="bdf86-210">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta logowania jednokrotnego Azure przyznać jej dostęp tooWizergos wydajności oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="bdf86-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Przypisz użytkownika][200]

<span data-ttu-id="bdf86-212">**tooassign tooWizergos Simona Britta oprogramowanie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bdf86-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdf86-213">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="bdf86-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][201]
2. <span data-ttu-id="bdf86-215">Z listy aplikacji hello wybierz **Wizergos oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="bdf86-217">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203]
4. <span data-ttu-id="bdf86-219">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="bdf86-220">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="bdf86-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="bdf86-222">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bdf86-222">Test single sign-on</span></span>
<span data-ttu-id="bdf86-223">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bdf86-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdf86-224">Po kliknięciu kafelka oprogramowanie Wizergos hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Wizergos wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bdf86-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdf86-225">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bdf86-225">Additional resources</span></span>
* [<span data-ttu-id="bdf86-226">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdf86-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdf86-227">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdf86-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
