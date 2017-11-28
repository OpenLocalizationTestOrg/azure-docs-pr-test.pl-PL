---
title: 'Samouczek: Integracji Azure Active Directory z Bynder | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="5ba65-103">Samouczek: Integracji Azure Active Directory z Bynder</span><span class="sxs-lookup"><span data-stu-id="5ba65-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="5ba65-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate Bynder w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ba65-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ba65-105">Integracja z usługą Azure AD Bynder zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5ba65-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="5ba65-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBynder</span><span class="sxs-lookup"><span data-stu-id="5ba65-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="5ba65-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBynder rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="5ba65-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5ba65-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="5ba65-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ba65-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ba65-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5ba65-110">Prerequisites</span></span>
<span data-ttu-id="5ba65-111">tooconfigure integracji z usługą Azure AD z Bynder należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5ba65-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="5ba65-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5ba65-113">Subskrypcja włączone Bynder jednokrotnego (SSO)</span><span class="sxs-lookup"><span data-stu-id="5ba65-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5ba65-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5ba65-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5ba65-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba65-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5ba65-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5ba65-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5ba65-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ba65-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ba65-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5ba65-118">Scenario description</span></span>
<span data-ttu-id="5ba65-119">Celem Hello tego samouczka jest tooenable możesz tootest Usługa rejestracji Jednokrotnej w Microsoft Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5ba65-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="5ba65-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5ba65-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ba65-121">Dodawanie Bynder z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5ba65-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="5ba65-122">Konfigurowanie i testowania Usługa rejestracji Jednokrotnej w Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="5ba65-123">Dodaj Bynder z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5ba65-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="5ba65-124">tooconfigure hello integracji Bynder do usługi Azure AD, należy tooadd Bynder z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5ba65-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ba65-125">**tooadd Bynder z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5ba65-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ba65-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="5ba65-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5ba65-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="5ba65-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="5ba65-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="5ba65-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="5ba65-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="5ba65-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="5ba65-135">W polu wyszukiwania hello wpisz **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-135">In hello search box, type **Bynder**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="5ba65-137">W panelu wyników hello, wybierz **Bynder**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba65-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Wybieranie aplikacji hello w galerii hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="5ba65-139">Konfiguracja i testowanie Usługa rejestracji Jednokrotnej w Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="5ba65-140">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowania programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5ba65-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ba65-141">Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w Bynder tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba65-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="5ba65-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Bynder musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5ba65-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="5ba65-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Bynder.</span><span class="sxs-lookup"><span data-stu-id="5ba65-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="5ba65-144">tooconfigure i testowania programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5ba65-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ba65-145">**[Konfigurowanie usługi Microsoft Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5ba65-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ba65-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Microsoft Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5ba65-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="5ba65-147">**[Tworzenie użytkownika testowego Bynder](#creating-a-bynder-test-user)**  -toohave odpowiednikiem Simona Britta w Bynder, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba65-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5ba65-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Simona Britta usługi Microsoft Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5ba65-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="5ba65-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5ba65-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="5ba65-150">Konfigurowanie logowania jednokrotnego usługi AD platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5ba65-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="5ba65-151">W tej sekcji można włączyć Usługa rejestracji Jednokrotnej w Microsoft Azure AD w klasycznym portalu hello i skonfigurować logowanie Jednokrotne w aplikacji Bynder.</span><span class="sxs-lookup"><span data-stu-id="5ba65-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="5ba65-152">**tooconfigure programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5ba65-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ba65-153">W klasycznym portalu hello na powitania **Bynder** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5ba65-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="5ba65-155">Na powitania **jak ma toosign użytkowników na tooBynder** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="5ba65-157">Na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, wykonaj następujące kroki hello i kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="5ba65-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="5ba65-159">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="5ba65-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="5ba65-160">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-160">Click **Next**.</span></span>
4. <span data-ttu-id="5ba65-161">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb** na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, a następnie kliknij polecenie hello **"Pokaż zaawansowane ustawienia (opcjonalnie)"**, a następnie wprowadź hello **na adres URL logowania** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="5ba65-163">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="5ba65-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="5ba65-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="5ba65-165">wartość Hello hello na adres URL logowania, w tym samouczku jest po prostu placeholfer.</span><span class="sxs-lookup"><span data-stu-id="5ba65-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="5ba65-166">tooget hello rzeczywiste vlaue dla danego środowiska, skontaktuj się z Bynder.</span><span class="sxs-lookup"><span data-stu-id="5ba65-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="5ba65-167">Na powitania **skonfigurować logowanie jednokrotne w Bynder** , wykonaj następujące kroki hello i kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="5ba65-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="5ba65-169">Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5ba65-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="5ba65-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-170">Click **Next**.</span></span>
6. <span data-ttu-id="5ba65-171">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Bynder.</span><span class="sxs-lookup"><span data-stu-id="5ba65-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="5ba65-172">Dołącz plik metadanych pobranych hello i udostępniać je tooset zespołu Bynder się rejestracji Jednokrotnej w bok.</span><span class="sxs-lookup"><span data-stu-id="5ba65-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="5ba65-173">W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]
8. <span data-ttu-id="5ba65-175">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5ba65-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-177">Create an Azure AD test user</span></span>
<span data-ttu-id="5ba65-178">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5ba65-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="5ba65-180">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5ba65-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ba65-181">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="5ba65-183">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5ba65-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="5ba65-184">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="5ba65-186">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="5ba65-188">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ba65-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="5ba65-190">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="5ba65-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="5ba65-191">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="5ba65-192">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-192">Click **Next**.</span></span>
6. <span data-ttu-id="5ba65-193">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ba65-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="5ba65-195">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="5ba65-196">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="5ba65-197">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="5ba65-198">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="5ba65-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-199">Click **Next**.</span></span>
7. <span data-ttu-id="5ba65-200">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="5ba65-202">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ba65-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="5ba65-204">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="5ba65-205">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="5ba65-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="5ba65-206">Tworzenie użytkownika testowego Bynder</span><span class="sxs-lookup"><span data-stu-id="5ba65-206">Create a Bynder test user</span></span>
<span data-ttu-id="5ba65-207">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Bynder.</span><span class="sxs-lookup"><span data-stu-id="5ba65-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="5ba65-208">Bynder obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="5ba65-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5ba65-209">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5ba65-209">There is no action item for you in this section.</span></span> <span data-ttu-id="5ba65-210">Nowy użytkownik zostanie utworzony podczas próby tooaccess Bynder, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5ba65-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="5ba65-211">Należy ręcznie toocreate użytkownika, należy najpierw toocontact hello Bynder z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="5ba65-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5ba65-212">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba65-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="5ba65-213">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure logowania jednokrotnego, przyznając jej tooBynder dostępu.</span><span class="sxs-lookup"><span data-stu-id="5ba65-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Przypisz użytkownika][200]

<span data-ttu-id="5ba65-215">**tooassign tooBynder Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5ba65-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ba65-216">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="5ba65-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][201]
2. <span data-ttu-id="5ba65-218">Z listy aplikacji hello wybierz **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="5ba65-220">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203]
4. <span data-ttu-id="5ba65-222">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="5ba65-223">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="5ba65-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="5ba65-225">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5ba65-225">Test single sign-on</span></span>
<span data-ttu-id="5ba65-226">Celem Hello w tej sekcji jest tootest Twojego systemu Microsoft Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5ba65-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ba65-227">Po kliknięciu kafelka Bynder hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Bynder aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5ba65-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ba65-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5ba65-228">Additional resources</span></span>
* [<span data-ttu-id="5ba65-229">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ba65-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ba65-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ba65-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
