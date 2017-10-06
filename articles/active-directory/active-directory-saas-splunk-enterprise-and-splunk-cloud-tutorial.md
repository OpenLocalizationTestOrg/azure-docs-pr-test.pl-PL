---
title: "Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługi Azure Active Directory i Splunk Enterprise i Splunk chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="1f77c-103">Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk</span><span class="sxs-lookup"><span data-stu-id="1f77c-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="1f77c-104">Z tego samouczka, dowiesz się, jak toointegrate Splunk przedsiębiorstwa i w chmurze Splunk w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f77c-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f77c-105">Integracja z usługą Azure AD Splunk przedsiębiorstwa i w chmurze Splunk zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1f77c-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f77c-106">TooSplunk Enterprise i Splunk chmury można kontrolować w usłudze Azure AD, który ma dostęp</span><span class="sxs-lookup"><span data-stu-id="1f77c-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="1f77c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSplunk przedsiębiorstwa i w chmurze Splunk rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f77c-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f77c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1f77c-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="1f77c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f77c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f77c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f77c-110">Prerequisites</span></span>

<span data-ttu-id="1f77c-111">tooconfigure integracji usługi Azure AD z Splunk przedsiębiorstwa i w chmurze Splunk należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1f77c-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="1f77c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f77c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f77c-113">Splunk Enterprise lub logowania jednokrotnego chmury Splunk włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1f77c-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="1f77c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1f77c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="1f77c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1f77c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f77c-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1f77c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1f77c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f77c-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1f77c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1f77c-118">Scenario description</span></span>
<span data-ttu-id="1f77c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1f77c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1f77c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1f77c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f77c-121">Dodawanie Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1f77c-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="1f77c-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f77c-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="1f77c-123">Dodaj Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1f77c-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="1f77c-124">tooconfigure hello integracji przedsiębiorstwa Splunk i Splunk chmury do usługi Azure AD, potrzebujesz tooadd Splunk przedsiębiorstwa oraz Splunk chmury hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1f77c-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f77c-125">**tooadd Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1f77c-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f77c-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1f77c-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="1f77c-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1f77c-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="1f77c-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="1f77c-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="1f77c-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="1f77c-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplikacje][4]

6. <span data-ttu-id="1f77c-135">W polu wyszukiwania hello wpisz **Splunk przedsiębiorstwa lub w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="1f77c-137">Wybierz w okienku wyników hello **Splunk przedsiębiorstwa i w chmurze Splunk**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1f77c-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1f77c-139">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1f77c-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1f77c-140">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1f77c-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f77c-141">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie hello odpowiednikiem użytkownik w organizacji Splunk i w chmurze Splunk jest tooa w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f77c-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="1f77c-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w organizacji Splunk i w chmurze Splunk musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1f77c-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="1f77c-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **nazwy użytkownika** Splunk przedsiębiorstwa i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="1f77c-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="1f77c-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i w chmurze Splunk, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1f77c-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f77c-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1f77c-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f77c-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1f77c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f77c-147">**[Tworzenie użytkownika testowego Splunk przedsiębiorstwa i w chmurze Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie Splunk i w chmurze Splunk, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f77c-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1f77c-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1f77c-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f77c-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1f77c-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1f77c-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1f77c-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1f77c-151">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w klasycznym portalu hello i konfigurowanie logowania jednokrotnego w aplikacji przedsiębiorstwa Splunk i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="1f77c-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="1f77c-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1f77c-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f77c-153">W klasycznym portalu hello na powitania **Splunk przedsiębiorstwa i w chmurze Splunk** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1f77c-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="1f77c-155">Na powitania **jak chcesz toosign użytkowników na tooSplunk przedsiębiorstwa i w chmurze Splunk** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="1f77c-157">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f77c-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="1f77c-159">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używane przez użytkowników na toosign tooyour Splunk przedsiębiorstwa i aplikacji w chmurze Splunk przy użyciu hello następującego wzorca:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="1f77c-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="1f77c-160">W hello **identyfikator** pole tekstowe, wprowadź adres URL powitania serwera Splunk.</span><span class="sxs-lookup"><span data-stu-id="1f77c-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="1f77c-161">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello z hello następującego wzorca:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="1f77c-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="1f77c-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="1f77c-163">Na powitania **skonfigurować logowanie jednokrotne w Splunk przedsiębiorstwa i w chmurze Splunk** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f77c-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="1f77c-165">Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1f77c-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="1f77c-166">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-166">Click **Next**.</span></span>

5. <span data-ttu-id="1f77c-167">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z Splunk przedsiębiorstwa i Splunk chmury z pomocą techniczną i podaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1f77c-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="1f77c-168">Witaj pobrane **federaton metadanych**</span><span class="sxs-lookup"><span data-stu-id="1f77c-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="1f77c-169">W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="1f77c-171">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1f77c-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f77c-173">Create an Azure AD test user</span></span>
<span data-ttu-id="1f77c-174">W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1f77c-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="1f77c-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1f77c-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f77c-177">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1f77c-179">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="1f77c-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="1f77c-180">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f77c-182">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1f77c-184">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f77c-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1f77c-186">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="1f77c-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1f77c-187">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1f77c-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-188">Click **Next**.</span></span>

6.  <span data-ttu-id="1f77c-189">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f77c-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="1f77c-191">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1f77c-192">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1f77c-193">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1f77c-194">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1f77c-195">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-195">Click **Next**.</span></span>

7. <span data-ttu-id="1f77c-196">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1f77c-198">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f77c-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="1f77c-200">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="1f77c-201">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="1f77c-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="1f77c-202">Tworzenie Splunk przedsiębiorstwa i chmury Splunk użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="1f77c-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="1f77c-203">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w przedsiębiorstwie Splunk i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="1f77c-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="1f77c-204">We współpracy z Splunk przedsiębiorstwa i w chmurze Splunk pomocy technicznej zespół tooadd hello użytkowników w hello Splunk Enterprise Splunk platforma i chmury.</span><span class="sxs-lookup"><span data-stu-id="1f77c-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1f77c-205">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f77c-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1f77c-206">W tej sekcji można włączyć toouse Simona Britta SSOy Azure udzielanie jej Enterprise tooSplunk dostępu i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="1f77c-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1f77c-208">**tooassign Simona Britta tooSplunk przedsiębiorstwa i Splunk chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1f77c-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f77c-209">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="1f77c-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1f77c-211">Z listy aplikacji hello wybierz **Splunk przedsiębiorstwa i w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="1f77c-213">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-213">In hello menu on hello top, click **Users**.</span></span>

    ![Przypisz użytkownika][203]

4. <span data-ttu-id="1f77c-215">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="1f77c-216">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="1f77c-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1f77c-218">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1f77c-218">Test single sign-on</span></span>

<span data-ttu-id="1f77c-219">W tej sekcji można przetestować programu Azure AD SSOonfiguration, przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1f77c-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="1f77c-220">Po kliknięciu hello Splunk przedsiębiorstwa i chmury Splunk kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Splunk przedsiębiorstwa i w chmurze Splunk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f77c-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1f77c-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1f77c-221">Additional resources</span></span>

* [<span data-ttu-id="1f77c-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f77c-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f77c-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f77c-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
