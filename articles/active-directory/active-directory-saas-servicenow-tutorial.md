---
title: "Samouczek: Integracji Azure Active Directory z usługi ServiceNow | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi ServiceNow i usługi ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="cbeff-103">Samouczek: Integracji Azure Active Directory z usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cbeff-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="cbeff-104">Z tego samouczka, dowiesz się, jak toointegrate usługi ServiceNow i Express usługi ServiceNow z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cbeff-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbeff-105">Integrowanie usługi ServiceNow i Express usługi ServiceNow z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cbeff-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="cbeff-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooServiceNow oraz usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="cbeff-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="cbeff-107">Użytkownicy tooautomatically get zalogowane tooServiceNow, a usługi ServiceNow Express (logowanie jednokrotne) można włączyć przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbeff-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="cbeff-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cbeff-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="cbeff-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cbeff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbeff-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cbeff-110">Prerequisites</span></span>
<span data-ttu-id="cbeff-111">tooconfigure integracji usługi Azure AD z usługi ServiceNow i usługi ServiceNow Express należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cbeff-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="cbeff-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbeff-112">An Azure AD subscription</span></span>
* <span data-ttu-id="cbeff-113">Dla usługi ServiceNow, wystąpienie lub dzierżawy usługi ServiceNow, wersja Calgary lub nowszej</span><span class="sxs-lookup"><span data-stu-id="cbeff-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="cbeff-114">Usługi ServiceNow Express, wystąpienie usługi ServiceNow Express, wersja Helsinkach lub nowszej</span><span class="sxs-lookup"><span data-stu-id="cbeff-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="cbeff-115">Dzierżawca usługi ServiceNow Hello musi mieć hello [wielu pojedynczy znak na dodatek dostawcy](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) włączone.</span><span class="sxs-lookup"><span data-stu-id="cbeff-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="cbeff-116">Można to zrobić [przesyłanie żądania obsługi](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="cbeff-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="cbeff-117">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="cbeff-118">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cbeff-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="cbeff-119">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cbeff-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="cbeff-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cbeff-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbeff-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cbeff-121">Scenario description</span></span>
<span data-ttu-id="cbeff-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cbeff-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbeff-123">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cbeff-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbeff-124">Dodawanie usługi ServiceNow z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cbeff-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="cbeff-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne dla usługi ServiceNow lub usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="cbeff-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="cbeff-126">Dodawanie usługi ServiceNow z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cbeff-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="cbeff-127">tooconfigure hello integracji usługi ServiceNow lub Express usługi ServiceNow z usługą Azure AD, należy tooadd usługi ServiceNow z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cbeff-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="cbeff-128">**tooadd usługi ServiceNow z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cbeff-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbeff-129">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="cbeff-131">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="cbeff-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cbeff-132">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="cbeff-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="cbeff-134">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="cbeff-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="cbeff-136">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="cbeff-138">W polu wyszukiwania hello wpisz **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="cbeff-140">Wybierz w okienku wyników hello **ServiceNow**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cbeff-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cbeff-142">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cbeff-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cbeff-143">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow lub Express usługi ServiceNow w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbeff-144">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ServiceNow jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbeff-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="cbeff-145">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi ServiceNow musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="cbeff-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="cbeff-146">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="cbeff-147">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cbeff-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cbeff-148">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cbeff-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cbeff-149">**[Konfigurowanie usługi Azure AD logowania jednokrotnego usługi ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cbeff-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="cbeff-150">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cbeff-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="cbeff-151">**[Tworzenie użytkownika testowego usługi ServiceNow](#creating-a-servicenow-test-user)**  -toohave odpowiednikiem Simona Britta w usługi ServiceNow, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbeff-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="cbeff-152">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cbeff-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="cbeff-153">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="cbeff-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="cbeff-154">Jeśli chcesz, aby tooconfigure ServiceNow pominąć krok 2.</span><span class="sxs-lookup"><span data-stu-id="cbeff-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="cbeff-155">Podobnie jeśli chcesz, aby tooconfigure Express usługi ServiceNow pominąć krok 1.</span><span class="sxs-lookup"><span data-stu-id="cbeff-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="cbeff-156">Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cbeff-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="cbeff-157">W klasycznym portalu usługi Azure AD hello na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego .</span><span class="sxs-lookup"><span data-stu-id="cbeff-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cbeff-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="cbeff-159">Na powitania **jak ma toosign użytkowników na tooServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cbeff-160">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="cbeff-161">Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="cbeff-162">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="cbeff-163">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-163">a.</span></span> <span data-ttu-id="cbeff-164">w hello **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="cbeff-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="cbeff-165">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-165">b.</span></span> <span data-ttu-id="cbeff-166">W hello **identyfikator** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="cbeff-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="cbeff-167">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-167">c.</span></span> <span data-ttu-id="cbeff-168">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="cbeff-168">Click **Next**</span></span>

4. <span data-ttu-id="cbeff-169">toohave usługi Azure AD automatycznie skonfigurować usługi ServiceNow dla uwierzytelniania opartego na SAML, wprowadź nazwę wystąpienia usługi ServiceNow, nazwa użytkownika i hasło administratora w hello **automatycznie skonfigurować logowanie jednokrotne** tworzą, a następnie kliknij przycisk  *Skonfiguruj*.</span><span class="sxs-lookup"><span data-stu-id="cbeff-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="cbeff-170">Należy pamiętać, że podana nazwa użytkownika administratora hello musi mieć hello **security_admin** rola przypisana w usługi ServiceNow dla tego toowork.</span><span class="sxs-lookup"><span data-stu-id="cbeff-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="cbeff-171">W przeciwnym razie toomanually skonfigurować usługi ServiceNow toouse usługi Azure AD jako dostawca tożsamości SAML, kliknij przycisk **ręcznie skonfigurować aplikacji hello dla logowania jednokrotnego**, następnie kliknij przycisk **dalej** i hello ukończone Poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="cbeff-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="cbeff-172">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="cbeff-173">Na powitania **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="cbeff-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="cbeff-174">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="cbeff-175">Zaloguj się na tooyour ServiceNow aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="cbeff-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="cbeff-176">Aktywuj hello *integracja — wiele pojedynczego logowania Instalatora dostawcy* wtyczki, wykonując hello następne kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="cbeff-177">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-177">a.</span></span> <span data-ttu-id="cbeff-178">W okienku nawigacji powitania po lewej stronie powitania Przejdź zbyt**definicji systemu** sekcji, a następnie kliknij przycisk **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="cbeff-179">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "aktywowanie wtyczki")</span><span class="sxs-lookup"><span data-stu-id="cbeff-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="cbeff-180">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-180">b.</span></span> <span data-ttu-id="cbeff-181">Wyszukaj *integracja — wiele pojedynczego logowania Instalatora dostawcy*.</span><span class="sxs-lookup"><span data-stu-id="cbeff-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="cbeff-182">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "aktywowanie wtyczki")</span><span class="sxs-lookup"><span data-stu-id="cbeff-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="cbeff-183">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-183">c.</span></span> <span data-ttu-id="cbeff-184">Wybierz wtyczki hello.</span><span class="sxs-lookup"><span data-stu-id="cbeff-184">Select hello plugin.</span></span> <span data-ttu-id="cbeff-185">Rigth kliknij i zaznacz **Aktywuj/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="cbeff-186">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-186">d.</span></span> <span data-ttu-id="cbeff-187">Kliknij przycisk hello **Aktywuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cbeff-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="cbeff-188">W okienku nawigacji hello po lewej stronie powitania kliknij **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="cbeff-189">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="cbeff-190">Na powitania **wiele właściwości logowania jednokrotnego dostawcy** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="cbeff-191">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="cbeff-192">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-192">a.</span></span> <span data-ttu-id="cbeff-193">Jako **włączyć wiele dostawcy logowania jednokrotnego**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="cbeff-194">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-194">b.</span></span> <span data-ttu-id="cbeff-195">Jako **włączania rejestrowania debugowania otrzymano hello dostawca wielu mechanizmów integracji logowania jednokrotnego**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="cbeff-196">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-196">c.</span></span> <span data-ttu-id="cbeff-197">W **tabeli pole hello na powitania użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="cbeff-198">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-198">d.</span></span> <span data-ttu-id="cbeff-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-199">Click **Save**.</span></span>

10. <span data-ttu-id="cbeff-200">W okienku nawigacji hello po lewej stronie powitania kliknij **certyfikaty x509**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="cbeff-201">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="cbeff-202">Na powitania **certyfikatów X.509** okna dialogowego, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="cbeff-203">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="cbeff-204">Na powitania **certyfikatów X.509** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="cbeff-205">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="cbeff-206">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-206">a.</span></span> <span data-ttu-id="cbeff-207">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-207">Click **New**.</span></span>
    
     <span data-ttu-id="cbeff-208">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-208">b.</span></span> <span data-ttu-id="cbeff-209">W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="cbeff-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="cbeff-210">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-210">c.</span></span> <span data-ttu-id="cbeff-211">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-211">Select **Active**.</span></span>
    
     <span data-ttu-id="cbeff-212">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-212">d.</span></span> <span data-ttu-id="cbeff-213">Jako **Format**, wybierz pozycję **PEM**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="cbeff-214">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-214">e.</span></span> <span data-ttu-id="cbeff-215">Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="cbeff-216">f.</span><span class="sxs-lookup"><span data-stu-id="cbeff-216">f.</span></span> <span data-ttu-id="cbeff-217">Otwórz z certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu PEM** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="cbeff-218">g.</span><span class="sxs-lookup"><span data-stu-id="cbeff-218">g.</span></span> <span data-ttu-id="cbeff-219">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-219">Click **Update**.</span></span>

13. <span data-ttu-id="cbeff-220">W okienku nawigacji hello po lewej stronie powitania kliknij **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="cbeff-221">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="cbeff-222">Na powitania **dostawców tożsamości** okna dialogowego, kliknij przycisk **nowy**:</span><span class="sxs-lookup"><span data-stu-id="cbeff-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="cbeff-223">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="cbeff-224">Na powitania **dostawców tożsamości** okna dialogowego, kliknij przycisk **aktualizację1 SAML2?**:</span><span class="sxs-lookup"><span data-stu-id="cbeff-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="cbeff-225">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="cbeff-226">W oknie dialogowym właściwości aktualizację1 SAML2 hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="cbeff-227">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="cbeff-228">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-228">a.</span></span> <span data-ttu-id="cbeff-229">w hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="cbeff-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="cbeff-230">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-230">b.</span></span> <span data-ttu-id="cbeff-231">W hello **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od tego, które pole służy toouniquely identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cbeff-232">Możesz tooemit configue usługi Azure AD albo identyfikator użytkownika hello Azure AD (główna nazwa użytkownika) lub hello adres e-mail jako hello Unikatowy identyfikator w tokenie SAML hello przez przejście toohello **usługi ServiceNow > atrybuty > logowanie jednokrotne** sekcji Witaj klasycznego portalu Azure i mapowanie hello potrzeby pola toohello **nameidentifier** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="cbeff-233">wartość Hello przechowywanych dla wybranego atrybutu hello w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości hello przechowywane w usługi ServiceNow hello wprowadzony w polu (np. nazwa_użytkownika)</span><span class="sxs-lookup"><span data-stu-id="cbeff-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="cbeff-234">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-234">c.</span></span> <span data-ttu-id="cbeff-235">W klasycznym portalu hello Azure AD, skopiuj hello **identyfikator dostawcy tożsamości** wartość, a następnie wklej go do hello **adres URL dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="cbeff-236">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-236">d.</span></span> <span data-ttu-id="cbeff-237">W klasycznym portalu hello Azure AD, skopiuj hello **adres URL żądania uwierzytelniania** wartość, a następnie wklej go do hello **AuthnRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="cbeff-238">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-238">e.</span></span> <span data-ttu-id="cbeff-239">W klasycznym portalu hello Azure AD, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="cbeff-240">f.</span><span class="sxs-lookup"><span data-stu-id="cbeff-240">f.</span></span> <span data-ttu-id="cbeff-241">W hello **strony głównej usługi ServiceNow** pole tekstowe, typ hello adres URL strony głównej wystąpienia usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cbeff-242">Strona główna wystąpienia usługi ServiceNow Hello jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="cbeff-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="cbeff-243">g.</span><span class="sxs-lookup"><span data-stu-id="cbeff-243">g.</span></span> <span data-ttu-id="cbeff-244">W hello **identyfikator podmiot / wystawca** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="cbeff-245">h.</span><span class="sxs-lookup"><span data-stu-id="cbeff-245">h.</span></span> <span data-ttu-id="cbeff-246">W hello **URL odbiorców** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="cbeff-247">i.</span><span class="sxs-lookup"><span data-stu-id="cbeff-247">i.</span></span> <span data-ttu-id="cbeff-248">W hello **powiązanie protokołu hello w rozszerzeniu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="cbeff-249">j.</span><span class="sxs-lookup"><span data-stu-id="cbeff-249">j.</span></span> <span data-ttu-id="cbeff-250">W hello zasad NameID pole tekstowe, wpisz **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="cbeff-251">k.</span><span class="sxs-lookup"><span data-stu-id="cbeff-251">k.</span></span> <span data-ttu-id="cbeff-252">Anuluj wybór **utworzyć AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="cbeff-253">l.</span><span class="sxs-lookup"><span data-stu-id="cbeff-253">l.</span></span> <span data-ttu-id="cbeff-254">W hello **metody AuthnContextClassRef**, typ `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="cbeff-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="cbeff-255">Jest to potrzebne tylko w przypadku organizacji tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cbeff-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="cbeff-256">Jeśli używasz lokalnych usług AD FS lub usługę MFA dla uwierzytelniania, a następnie ta wartość nie należy konfigurować.</span><span class="sxs-lookup"><span data-stu-id="cbeff-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="cbeff-257">m.</span><span class="sxs-lookup"><span data-stu-id="cbeff-257">m.</span></span> <span data-ttu-id="cbeff-258">W **pochylanie zegara** pole tekstowe, typ **60**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="cbeff-259">n.</span><span class="sxs-lookup"><span data-stu-id="cbeff-259">n.</span></span> <span data-ttu-id="cbeff-260">Jako **pojedynczy znak na skrypt**, wybierz pozycję **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="cbeff-261">o.</span><span class="sxs-lookup"><span data-stu-id="cbeff-261">o.</span></span> <span data-ttu-id="cbeff-262">Jako **x509 certyfikatu**, wybierz pozycję hello certyfikat został utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="cbeff-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="cbeff-263">p.</span><span class="sxs-lookup"><span data-stu-id="cbeff-263">p.</span></span> <span data-ttu-id="cbeff-264">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="cbeff-265">W portalu klasycznym hello Azure AD, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="cbeff-266">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="cbeff-267">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="cbeff-268">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="cbeff-269">Konfigurowanie usługi Azure AD jednokrotnej usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="cbeff-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="cbeff-270">W klasycznym portalu usługi Azure AD hello na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego .</span><span class="sxs-lookup"><span data-stu-id="cbeff-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cbeff-271">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="cbeff-272">Na powitania **jak ma toosign użytkowników na tooServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cbeff-273">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="cbeff-274">Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="cbeff-275">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="cbeff-276">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-276">a.</span></span> <span data-ttu-id="cbeff-277">w hello **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="cbeff-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="cbeff-278">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-278">b.</span></span> <span data-ttu-id="cbeff-279">W hello **adres URL wystawcy** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="cbeff-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="cbeff-280">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-280">c.</span></span> <span data-ttu-id="cbeff-281">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="cbeff-281">Click **Next**</span></span>

4. <span data-ttu-id="cbeff-282">Kliknij przycisk **ręcznie skonfigurować aplikacji hello dla logowania jednokrotnego**, następnie kliknij przycisk **dalej** i pełne hello wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="cbeff-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="cbeff-283">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="cbeff-284">Na powitania **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu hello lokalnie na komputerze, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="cbeff-285">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="cbeff-286">Zaloguj się na tooyour aplikacji Express usługi ServiceNow jako administrator.</span><span class="sxs-lookup"><span data-stu-id="cbeff-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="cbeff-287">W okienku nawigacji hello po lewej stronie powitania kliknij **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="cbeff-288">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="cbeff-289">Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij ikonę konfiguracji hello na wielką hello prawo i ustaw hello następujących właściwości:</span><span class="sxs-lookup"><span data-stu-id="cbeff-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="cbeff-290">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cbeff-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="cbeff-291">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-291">a.</span></span> <span data-ttu-id="cbeff-292">Przełącz **włączyć wiele dostawcy logowania jednokrotnego** toohello prawo.</span><span class="sxs-lookup"><span data-stu-id="cbeff-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="cbeff-293">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-293">b.</span></span> <span data-ttu-id="cbeff-294">Przełącz **debugowania Włącz rejestrowanie dla hello dostawca wielu mechanizmów integracji logowania jednokrotnego** toohello prawo.</span><span class="sxs-lookup"><span data-stu-id="cbeff-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="cbeff-295">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-295">c.</span></span> <span data-ttu-id="cbeff-296">W **tabeli pole hello na powitania użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="cbeff-297">Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="cbeff-298">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="cbeff-299">Na powitania **certyfikatów X.509** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="cbeff-300">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="cbeff-301">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-301">a.</span></span> <span data-ttu-id="cbeff-302">W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="cbeff-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="cbeff-303">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-303">b.</span></span> <span data-ttu-id="cbeff-304">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-304">Select **Active**.</span></span>
    
    <span data-ttu-id="cbeff-305">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-305">c.</span></span> <span data-ttu-id="cbeff-306">Jako **Format**, wybierz pozycję **PEM**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="cbeff-307">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-307">d.</span></span> <span data-ttu-id="cbeff-308">Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="cbeff-309">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-309">e.</span></span> <span data-ttu-id="cbeff-310">Utwórz plik kodowany w standardzie Base64 z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cbeff-311">Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="cbeff-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="cbeff-312">f.</span><span class="sxs-lookup"><span data-stu-id="cbeff-312">f.</span></span> <span data-ttu-id="cbeff-313">Otwórz z certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu PEM** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="cbeff-314">g.</span><span class="sxs-lookup"><span data-stu-id="cbeff-314">g.</span></span> <span data-ttu-id="cbeff-315">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-315">Click **Update**.</span></span>
11. <span data-ttu-id="cbeff-316">Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowe IdP**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="cbeff-317">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="cbeff-318">Na powitania **Dodaj nowego dostawcę tożsamości** okna dialogowego, w obszarze **Konfigurowanie dostawcy tożsamości**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="cbeff-319">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="cbeff-320">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-320">a.</span></span> <span data-ttu-id="cbeff-321">w hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="cbeff-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="cbeff-322">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-322">b.</span></span> <span data-ttu-id="cbeff-323">W klasycznym portalu hello Azure AD, skopiuj hello **identyfikator dostawcy tożsamości** wartość, a następnie wklej go do hello **adres URL dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="cbeff-324">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-324">c.</span></span> <span data-ttu-id="cbeff-325">W klasycznym portalu hello Azure AD, skopiuj hello **adres URL żądania uwierzytelniania** wartość, a następnie wklej go do hello **AuthnRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="cbeff-326">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-326">d.</span></span> <span data-ttu-id="cbeff-327">W klasycznym portalu hello Azure AD, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cbeff-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="cbeff-328">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-328">e.</span></span> <span data-ttu-id="cbeff-329">Jako **certyfikat dostawcy tożsamości**, wybierz pozycję hello certyfikat został utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="cbeff-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="cbeff-330">Kliknij przycisk **Zaawansowane ustawienia**, a następnie w obszarze **dodatkowe właściwości dostawcy tożsamości**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="cbeff-331">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="cbeff-332">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-332">a.</span></span> <span data-ttu-id="cbeff-333">W hello **powiązanie protokołu hello w rozszerzeniu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="cbeff-334">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-334">b.</span></span> <span data-ttu-id="cbeff-335">W hello **zasad NameID** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="cbeff-336">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-336">c.</span></span> <span data-ttu-id="cbeff-337">W hello **metody AuthnContextClassRef**, typ **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="cbeff-338">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-338">d.</span></span> <span data-ttu-id="cbeff-339">Anuluj wybór **utworzyć AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="cbeff-340">W obszarze **dodatkowe właściwości dostawcy usług**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="cbeff-341">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="cbeff-342">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-342">a.</span></span> <span data-ttu-id="cbeff-343">W hello **strony głównej usługi ServiceNow** pole tekstowe, typ hello adres URL strony głównej wystąpienia usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="cbeff-344">Strona główna wystąpienia usługi ServiceNow Hello jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="cbeff-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="cbeff-345">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-345">b.</span></span> <span data-ttu-id="cbeff-346">W hello **identyfikator podmiot / wystawca** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="cbeff-347">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-347">c.</span></span> <span data-ttu-id="cbeff-348">W hello **identyfikatora URI odbiorców** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="cbeff-349">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-349">d.</span></span> <span data-ttu-id="cbeff-350">W **pochylanie zegara** pole tekstowe, typ **60**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="cbeff-351">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-351">e.</span></span> <span data-ttu-id="cbeff-352">W hello **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od tego, które pole służy toouniquely identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="cbeff-353">Możesz tooemit configue usługi Azure AD albo identyfikator użytkownika hello Azure AD (główna nazwa użytkownika) lub hello adres e-mail jako hello Unikatowy identyfikator w tokenie SAML hello przez przejście toohello **usługi ServiceNow > atrybuty > logowanie jednokrotne** sekcji Witaj klasycznego portalu Azure i mapowanie hello potrzeby pola toohello **nameidentifier** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="cbeff-354">wartość Hello przechowywanych dla wybranego atrybutu hello w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości hello przechowywane w usługi ServiceNow hello wprowadzony w polu (np. nazwa_użytkownika)</span><span class="sxs-lookup"><span data-stu-id="cbeff-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="cbeff-355">f.</span><span class="sxs-lookup"><span data-stu-id="cbeff-355">f.</span></span> <span data-ttu-id="cbeff-356">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-356">Click **Save**.</span></span> 

3. <span data-ttu-id="cbeff-357">W portalu klasycznym hello Azure AD, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="cbeff-358">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="cbeff-359">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="cbeff-360">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cbeff-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="cbeff-361">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="cbeff-361">Configuring user provisioning</span></span>
<span data-ttu-id="cbeff-362">Celem Hello w tej sekcji jest toooutline jak tooServiceNow kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbeff-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="cbeff-363">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cbeff-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="cbeff-364">Hello Azure classic Portal zarządzania, na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="cbeff-365">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="cbeff-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="cbeff-366">Na powitania **Wprowadź użytkownika usługi ServiceNow poświadczenia tooenable automatyczne Inicjowanie obsługi użytkowników** Podaj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="cbeff-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="cbeff-367">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-367">a.</span></span> <span data-ttu-id="cbeff-368">W hello **nazwy wystąpienia usługi ServiceNow** pole tekstowe, nazwę wystąpienia usługi ServiceNow hello typu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="cbeff-369">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-369">b.</span></span> <span data-ttu-id="cbeff-370">W hello **nazwa użytkownika administratora usługi ServiceNow** pole tekstowe, nazwa typu hello hello konta administratora usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="cbeff-371">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-371">c.</span></span> <span data-ttu-id="cbeff-372">W hello **hasło administratora usługi ServiceNow** tekstowym, wpisz hello hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="cbeff-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="cbeff-373">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-373">d.</span></span> <span data-ttu-id="cbeff-374">Kliknij przycisk **zweryfikować** tooverify konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cbeff-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="cbeff-375">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-375">e.</span></span> <span data-ttu-id="cbeff-376">Kliknij przycisk hello **dalej** hello tooopen przycisk **następne kroki** strony.</span><span class="sxs-lookup"><span data-stu-id="cbeff-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="cbeff-377">f.</span><span class="sxs-lookup"><span data-stu-id="cbeff-377">f.</span></span> <span data-ttu-id="cbeff-378">Tooprovision wszystkich użytkowników toothis aplikacji, wybierz opcję "**automatycznie obsługiwać wszystkich kont użytkowników w aplikacji toothis katalogu hello**".</span><span class="sxs-lookup"><span data-stu-id="cbeff-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="cbeff-379">![Następne kroki](./media/active-directory-saas-servicenow-tutorial/IC698804.png "następne kroki")</span><span class="sxs-lookup"><span data-stu-id="cbeff-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="cbeff-380">g.</span><span class="sxs-lookup"><span data-stu-id="cbeff-380">g.</span></span> <span data-ttu-id="cbeff-381">Na powitania **następne kroki** kliknij przycisk **Complete** toosave konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cbeff-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cbeff-382">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbeff-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="cbeff-383">W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cbeff-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="cbeff-385">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cbeff-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbeff-386">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="cbeff-388">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="cbeff-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="cbeff-389">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cbeff-391">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="cbeff-393">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="cbeff-395">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-395">a.</span></span> <span data-ttu-id="cbeff-396">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cbeff-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="cbeff-397">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-397">b.</span></span> <span data-ttu-id="cbeff-398">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="cbeff-399">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-399">c.</span></span> <span data-ttu-id="cbeff-400">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-400">Click **Next**.</span></span>

6. <span data-ttu-id="cbeff-401">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="cbeff-403">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-403">a.</span></span> <span data-ttu-id="cbeff-404">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="cbeff-405">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-405">b.</span></span> <span data-ttu-id="cbeff-406">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="cbeff-407">c.</span><span class="sxs-lookup"><span data-stu-id="cbeff-407">c.</span></span> <span data-ttu-id="cbeff-408">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="cbeff-409">d.</span><span class="sxs-lookup"><span data-stu-id="cbeff-409">d.</span></span> <span data-ttu-id="cbeff-410">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="cbeff-411">e.</span><span class="sxs-lookup"><span data-stu-id="cbeff-411">e.</span></span> <span data-ttu-id="cbeff-412">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-412">Click **Next**.</span></span>

7. <span data-ttu-id="cbeff-413">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="cbeff-415">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cbeff-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="cbeff-417">a.</span><span class="sxs-lookup"><span data-stu-id="cbeff-417">a.</span></span> <span data-ttu-id="cbeff-418">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="cbeff-419">b.</span><span class="sxs-lookup"><span data-stu-id="cbeff-419">b.</span></span> <span data-ttu-id="cbeff-420">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="cbeff-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="cbeff-421">Tworzenie użytkownika testowego usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="cbeff-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="cbeff-422">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="cbeff-423">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="cbeff-424">Jeśli nie wiesz, jak tooadd w ServiceNow lub Express usługi ServiceNow konta użytkownika, skontaktuj się z zespołem pomocy technicznej usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="cbeff-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cbeff-425">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbeff-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="cbeff-426">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooServiceNow dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cbeff-428">**tooassign tooServiceNow Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cbeff-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbeff-429">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="cbeff-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cbeff-431">Z listy aplikacji hello wybierz **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="cbeff-433">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 

4. <span data-ttu-id="cbeff-435">Na liście hello wszystkich użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="cbeff-436">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="cbeff-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="cbeff-438">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cbeff-438">Testing single sign-on</span></span>
<span data-ttu-id="cbeff-439">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbeff-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cbeff-440">Po kliknięciu kafelka usługi ServiceNow hello w hello panelu dostępu należy pobrać aplikację usługi ServiceNow tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="cbeff-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbeff-441">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cbeff-441">Additional resources</span></span>
* [<span data-ttu-id="cbeff-442">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbeff-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbeff-443">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cbeff-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
