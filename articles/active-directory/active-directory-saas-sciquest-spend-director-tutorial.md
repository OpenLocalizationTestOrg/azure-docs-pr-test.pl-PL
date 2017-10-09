---
title: "Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SciQuest spędzają na katalog."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="715df-103">Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog</span><span class="sxs-lookup"><span data-stu-id="715df-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="715df-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate SciQuest spędzają na katalog z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="715df-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="715df-105">Integracja z usługą Azure AD SciQuest spędzają na katalog zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="715df-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="715df-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSciQuest Dyrektor wydatków</span><span class="sxs-lookup"><span data-stu-id="715df-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="715df-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSciQuest Dyrektor wydatków (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="715df-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="715df-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="715df-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="715df-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="715df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="715df-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="715df-110">Prerequisites</span></span>
<span data-ttu-id="715df-111">tooconfigure integracji usługi Azure AD z SciQuest spędzają na katalog, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="715df-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="715df-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="715df-112">An Azure AD subscription</span></span>
* <span data-ttu-id="715df-113">Dyrektor spędzają SciQuest jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="715df-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="715df-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="715df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="715df-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="715df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="715df-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="715df-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="715df-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="715df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="715df-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="715df-118">Scenario Description</span></span>
<span data-ttu-id="715df-119">Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="715df-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="715df-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="715df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="715df-121">Dodawanie SciQuest spędzają na katalog z galerii hello</span><span class="sxs-lookup"><span data-stu-id="715df-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="715df-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="715df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="715df-123">Dodawanie SciQuest spędzają na katalog z galerii hello</span><span class="sxs-lookup"><span data-stu-id="715df-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="715df-124">tooconfigure hello integracji SciQuest spędzają na katalog usługi Azure AD, należy tooadd SciQuest spędzają na katalog z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="715df-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="715df-125">**tooadd SciQuest spędzają na katalog z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="715df-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="715df-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="715df-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="715df-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="715df-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="715df-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="715df-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="715df-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="715df-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="715df-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="715df-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="715df-135">W polu wyszukiwania hello wpisz **sciQuest spędzają na katalog**.</span><span class="sxs-lookup"><span data-stu-id="715df-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="715df-137">Wybierz w okienku wyników hello **SciQuest spędzają na katalog**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="715df-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplikacje][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="715df-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="715df-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="715df-140">Celem Hello w tej sekcji jest tooshow jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SciQuest Dyrektor spędzają na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="715df-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="715df-141">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w SciQuest spędzają na katalog tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="715df-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="715df-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SciQuest spędzają na katalog musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="715df-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="715df-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="715df-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="715df-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="715df-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="715df-145">**[Konfigurowanie usługi Azure AD pojedynczego rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="715df-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="715df-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="715df-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="715df-147">**[Tworzenie użytkownika testowego SciQuest spędzają na katalog](#creating-a-halogen-software-test-user)**  -toohave odpowiednikiem Simona Britta w spędzają na katalog SciQuest, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="715df-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="715df-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="715df-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="715df-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="715df-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="715df-150">Konfigurowanie usługi Azure AD pojedynczej rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="715df-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="715df-151">Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w SciQuest spędzają na katalog aplikacji.</span><span class="sxs-lookup"><span data-stu-id="715df-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="715df-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="715df-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="715df-153">W hello klasycznego portalu Azure na powitania **SciQuest spędzają na katalog** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="715df-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. <span data-ttu-id="715df-155">Na powitania **jak ma toosign użytkowników na tooSciQuest Dyrektor wydatków** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="715df-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]

3. <span data-ttu-id="715df-157">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="715df-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][10]
   
     <span data-ttu-id="715df-159">a.</span><span class="sxs-lookup"><span data-stu-id="715df-159">a.</span></span> <span data-ttu-id="715df-160">W hello **na adres URL logowania** tekstowym, wpisz adres URL używany przez Twoje toosign użytkowników na tooyour SciQuest spędzają na katalog aplikacji przy użyciu następującego wzorca hello: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="715df-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="715df-161">b.</span><span class="sxs-lookup"><span data-stu-id="715df-161">b.</span></span> <span data-ttu-id="715df-162">W hello **adres URL odpowiedzi** pole tekstowe, typ hello takie same wartości zostały wpisane w hello **na adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="715df-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="715df-163">c.</span><span class="sxs-lookup"><span data-stu-id="715df-163">c.</span></span> <span data-ttu-id="715df-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="715df-164">Click **Next**.</span></span>

4. <span data-ttu-id="715df-165">Na powitania **skonfigurować logowanie jednokrotne w SciQuest spędzają na katalog** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="715df-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Co to jest program Azure AD Connect][11]

5. <span data-ttu-id="715df-167">Skontaktuj się z SciQuest tooenable obsługi tej metody uwierzytelniania przy użyciu metadanych hello powyżej pobrane.</span><span class="sxs-lookup"><span data-stu-id="715df-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="715df-168">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="715df-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Co to jest program Azure AD Connect][15]

7. <span data-ttu-id="715df-170">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="715df-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="715df-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="715df-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="715df-172">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="715df-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="715df-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="715df-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="715df-174">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="715df-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Co to jest program Azure AD Connect][100] 

2. <span data-ttu-id="715df-176">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="715df-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="715df-177">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="715df-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][101] 

4. <span data-ttu-id="715df-179">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="715df-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Co to jest program Azure AD Connect][102] 

5. <span data-ttu-id="715df-181">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="715df-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][103] 
   
    <span data-ttu-id="715df-183">a.</span><span class="sxs-lookup"><span data-stu-id="715df-183">a.</span></span> <span data-ttu-id="715df-184">Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.</span><span class="sxs-lookup"><span data-stu-id="715df-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="715df-185">b.</span><span class="sxs-lookup"><span data-stu-id="715df-185">b.</span></span> <span data-ttu-id="715df-186">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="715df-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="715df-187">c.</span><span class="sxs-lookup"><span data-stu-id="715df-187">c.</span></span> <span data-ttu-id="715df-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="715df-188">Click **Next**.</span></span>

6. <span data-ttu-id="715df-189">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="715df-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Co to jest program Azure AD Connect][104] 
   
    <span data-ttu-id="715df-191">a.</span><span class="sxs-lookup"><span data-stu-id="715df-191">a.</span></span> <span data-ttu-id="715df-192">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="715df-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="715df-193">b.</span><span class="sxs-lookup"><span data-stu-id="715df-193">b.</span></span> <span data-ttu-id="715df-194">W hello **nazwisko** txtbox, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="715df-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="715df-195">c.</span><span class="sxs-lookup"><span data-stu-id="715df-195">c.</span></span> <span data-ttu-id="715df-196">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="715df-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="715df-197">d.</span><span class="sxs-lookup"><span data-stu-id="715df-197">d.</span></span> <span data-ttu-id="715df-198">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="715df-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="715df-199">e.</span><span class="sxs-lookup"><span data-stu-id="715df-199">e.</span></span> <span data-ttu-id="715df-200">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="715df-200">Click **Next**.</span></span>

7. <span data-ttu-id="715df-201">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="715df-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Co to jest program Azure AD Connect][105]  

8. <span data-ttu-id="715df-203">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="715df-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][106]   
   
    <span data-ttu-id="715df-205">a.</span><span class="sxs-lookup"><span data-stu-id="715df-205">a.</span></span> <span data-ttu-id="715df-206">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="715df-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="715df-207">b.</span><span class="sxs-lookup"><span data-stu-id="715df-207">b.</span></span> <span data-ttu-id="715df-208">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="715df-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="715df-209">Tworzenie użytkownika testowego SciQuest spędzają na katalog</span><span class="sxs-lookup"><span data-stu-id="715df-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="715df-210">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="715df-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="715df-211">Należy toocontact z zespołem pomocy technicznej SciQuest spędzają na katalog i podaj szczegóły hello o tooget konta użytkownika testu, on utworzony.</span><span class="sxs-lookup"><span data-stu-id="715df-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="715df-212">Alternatywnie można też skorzystać w czasie inicjowania obsługi administracyjnej, pojedynczego logowania jednokrotnego funkcja, która jest obsługiwana przez SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="715df-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="715df-213">Po włączeniu w czasie inicjowania obsługi użytkowników są tworzone automatycznie przez SciQuest spędzają na katalog podczas jednego próba logowania jednokrotnego, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="715df-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="715df-214">Ta funkcja eliminuje konieczność hello toomanually tworzenie odpowiednikiem rejestracji jednokrotnej użytkowników.</span><span class="sxs-lookup"><span data-stu-id="715df-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="715df-215">tooget w czasie inicjowania obsługi administracyjnej włączone, ale trzeba toocontact jest zespołem pomocy technicznej SciQuest spędzają na katalog.</span><span class="sxs-lookup"><span data-stu-id="715df-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="715df-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="715df-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="715df-217">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSciQuest dostępu Dyrektor wydatków.</span><span class="sxs-lookup"><span data-stu-id="715df-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Co to jest program Azure AD Connect][200]

<span data-ttu-id="715df-219">**tooassign tooSciQuest Simona Britta dyrektora wydatków, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="715df-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="715df-220">Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="715df-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Co to jest program Azure AD Connect][201]

2. <span data-ttu-id="715df-222">Z listy aplikacji hello wybierz **SciQuest spędzają na katalog**.</span><span class="sxs-lookup"><span data-stu-id="715df-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Co to jest program Azure AD Connect][202]

3. <span data-ttu-id="715df-224">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="715df-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][203]

4. <span data-ttu-id="715df-226">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="715df-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Co to jest program Azure AD Connect][204]

5. <span data-ttu-id="715df-228">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="715df-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Co to jest program Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="715df-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="715df-230">Testing Single Sign-On</span></span>
<span data-ttu-id="715df-231">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="715df-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="715df-232">Po kliknięciu kafelka SciQuest spędzają na katalog hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SciQuest spędzają na katalog aplikacji.</span><span class="sxs-lookup"><span data-stu-id="715df-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="715df-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="715df-233">Additional Resources</span></span>
* [<span data-ttu-id="715df-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="715df-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="715df-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="715df-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

