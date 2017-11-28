---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Soonr | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Soonr w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="7608a-103">Samouczek: Integracji Azure Active Directory z Soonr w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="7608a-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="7608a-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate Soonr pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7608a-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7608a-105">Integrowanie Soonr miejsca pracy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7608a-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7608a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSoonr miejsca pracy</span><span class="sxs-lookup"><span data-stu-id="7608a-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="7608a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSoonr pracy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7608a-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7608a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7608a-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="7608a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7608a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7608a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7608a-110">Prerequisites</span></span>

<span data-ttu-id="7608a-111">tooconfigure integracji usługi Azure AD z miejsca pracy Soonr należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7608a-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="7608a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7608a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7608a-113">Obszar roboczy Soonr jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7608a-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="7608a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7608a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7608a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7608a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7608a-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7608a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7608a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7608a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7608a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7608a-118">Scenario description</span></span>
<span data-ttu-id="7608a-119">Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7608a-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7608a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7608a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7608a-121">Dodawanie miejsca pracy Soonr z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7608a-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="7608a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7608a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="7608a-123">Dodawanie miejsca pracy Soonr z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7608a-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="7608a-124">tooconfigure hello integracji Soonr dołączanie do usługi Azure AD, należy tooadd Soonr miejsca pracy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7608a-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7608a-125">**tooadd Soonr w miejscu pracy na powitania galerii, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7608a-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7608a-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7608a-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7608a-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="7608a-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7608a-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="7608a-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="7608a-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="7608a-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="7608a-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="7608a-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Aplikacje][4]

6. <span data-ttu-id="7608a-135">W polu wyszukiwania hello wpisz **pracy Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7608a-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="7608a-137">Wybierz w okienku wyników hello **Soonr w miejscu pracy**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7608a-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7608a-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7608a-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7608a-140">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7608a-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7608a-141">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w miejscu pracy Soonr tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7608a-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="7608a-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy Soonr musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7608a-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="7608a-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy Soonr.</span><span class="sxs-lookup"><span data-stu-id="7608a-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="7608a-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7608a-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7608a-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7608a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7608a-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7608a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7608a-147">**[Tworzenie użytkownika testowego pracy Soonr](#creating-a-soonr-workplace-test-user)**  -toohave odpowiednikiem Simona Britta w miejscu pracy Soonr, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7608a-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7608a-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7608a-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7608a-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7608a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7608a-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7608a-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7608a-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w miejscu pracy Soonr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7608a-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="7608a-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7608a-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7608a-153">W hello klasycznego portalu Azure na powitania **pracy Soonr** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7608a-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="7608a-155">Na powitania **jak ma toosign użytkowników w miejscu pracy tooSoonr** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7608a-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="7608a-157">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj następujące kroki hello:.</span><span class="sxs-lookup"><span data-stu-id="7608a-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="7608a-159">a.</span><span class="sxs-lookup"><span data-stu-id="7608a-159">a.</span></span> <span data-ttu-id="7608a-160">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="7608a-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="7608a-161">b.</span><span class="sxs-lookup"><span data-stu-id="7608a-161">b.</span></span> <span data-ttu-id="7608a-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7608a-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7608a-163">Należy pamiętać, że nie jest hello rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="7608a-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="7608a-164">Masz tooupdate tej wartości z rzeczywistego hello Zaloguj się na adres URL.</span><span class="sxs-lookup"><span data-stu-id="7608a-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="7608a-165">Skontaktuj się z tooget zespołu pomocy technicznej pracy Soonr tej wartości.</span><span class="sxs-lookup"><span data-stu-id="7608a-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="7608a-166">Na powitania **skonfigurować logowanie jednokrotne w miejscu pracy Soonr** kliknij przycisk **pobierania metadanych** , a następnie zapisz plik hello na tym komputerze:</span><span class="sxs-lookup"><span data-stu-id="7608a-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="7608a-168">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Soonr miejsca pracy i podaj następujący hello:</span><span class="sxs-lookup"><span data-stu-id="7608a-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="7608a-169">• hello pobrane **metadanych** pliku</span><span class="sxs-lookup"><span data-stu-id="7608a-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="7608a-170">• hello **adres URL wystawcy**</span><span class="sxs-lookup"><span data-stu-id="7608a-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="7608a-171">• hello **adres URL logowania jednokrotnego SAML**</span><span class="sxs-lookup"><span data-stu-id="7608a-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="7608a-172">• hello **pojedynczy adres URL usługi Sign-Out**</span><span class="sxs-lookup"><span data-stu-id="7608a-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="7608a-173">Ta aplikacja została zastąpiona nowszą <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">pracy Autotask</a> i może odnosić się <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">to</a> samouczka do konfigurowania aplikacji hello z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7608a-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="7608a-174">W hello klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7608a-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="7608a-176">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7608a-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD rejestracji jednokrotnej][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7608a-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7608a-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="7608a-179">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7608a-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="7608a-181">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7608a-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7608a-182">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7608a-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="7608a-184">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="7608a-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7608a-185">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7608a-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7608a-187">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7608a-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7608a-189">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7608a-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="7608a-191">a.</span><span class="sxs-lookup"><span data-stu-id="7608a-191">a.</span></span> <span data-ttu-id="7608a-192">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="7608a-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="7608a-193">b.</span><span class="sxs-lookup"><span data-stu-id="7608a-193">b.</span></span> <span data-ttu-id="7608a-194">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7608a-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7608a-195">c.</span><span class="sxs-lookup"><span data-stu-id="7608a-195">c.</span></span> <span data-ttu-id="7608a-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7608a-196">Click **Next**.</span></span>

6.  <span data-ttu-id="7608a-197">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7608a-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="7608a-199">a.</span><span class="sxs-lookup"><span data-stu-id="7608a-199">a.</span></span> <span data-ttu-id="7608a-200">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7608a-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="7608a-201">b.</span><span class="sxs-lookup"><span data-stu-id="7608a-201">b.</span></span> <span data-ttu-id="7608a-202">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="7608a-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="7608a-203">c.</span><span class="sxs-lookup"><span data-stu-id="7608a-203">c.</span></span> <span data-ttu-id="7608a-204">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="7608a-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="7608a-205">d.</span><span class="sxs-lookup"><span data-stu-id="7608a-205">d.</span></span> <span data-ttu-id="7608a-206">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7608a-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="7608a-207">e.</span><span class="sxs-lookup"><span data-stu-id="7608a-207">e.</span></span> <span data-ttu-id="7608a-208">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7608a-208">Click **Next**.</span></span>

7. <span data-ttu-id="7608a-209">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="7608a-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7608a-211">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7608a-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="7608a-213">a.</span><span class="sxs-lookup"><span data-stu-id="7608a-213">a.</span></span> <span data-ttu-id="7608a-214">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="7608a-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="7608a-215">b.</span><span class="sxs-lookup"><span data-stu-id="7608a-215">b.</span></span> <span data-ttu-id="7608a-216">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7608a-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="7608a-217">Tworzenie użytkownika testowego Soonr w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="7608a-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="7608a-218">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w miejscu pracy Soonr.</span><span class="sxs-lookup"><span data-stu-id="7608a-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="7608a-219">Należy skontaktować się z toocreate zespołu pomocy technicznej Soonr w miejscu pracy użytkownika hello platformy.</span><span class="sxs-lookup"><span data-stu-id="7608a-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="7608a-220">Można zwiększyć hello biletu pomocy technicznej z Soonr z <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">tutaj</a>.</span><span class="sxs-lookup"><span data-stu-id="7608a-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7608a-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7608a-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7608a-222">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSoonr dostępu do miejsca pracy.</span><span class="sxs-lookup"><span data-stu-id="7608a-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7608a-224">**tooassign tooSoonr Simona Britta miejsca pracy, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7608a-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7608a-225">Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="7608a-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7608a-227">Z listy aplikacji hello wybierz **pracy Soonr**.</span><span class="sxs-lookup"><span data-stu-id="7608a-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="7608a-229">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7608a-229">In hello menu on hello top, click **Users**.</span></span>

    ![Przypisz użytkownika][203] 

1. <span data-ttu-id="7608a-231">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="7608a-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="7608a-232">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="7608a-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="7608a-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7608a-234">Testing single sign-on</span></span>

<span data-ttu-id="7608a-235">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7608a-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7608a-236">Po kliknięciu hello pracy Soonr kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Soonr pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7608a-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7608a-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7608a-237">Additional resources</span></span>

* [<span data-ttu-id="7608a-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7608a-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7608a-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7608a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
