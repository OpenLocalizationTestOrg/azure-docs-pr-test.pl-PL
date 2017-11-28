---
title: 'Samouczek: Integracji Azure Active Directory z AirWatch | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="d0c92-103">Samouczek: Integracji Azure Active Directory z AirWatch</span><span class="sxs-lookup"><span data-stu-id="d0c92-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="d0c92-104">Z tego samouczka, dowiesz się, jak toointegrate AirWatch w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0c92-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c92-105">Integracja z usługą Azure AD AirWatch zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d0c92-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0c92-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="d0c92-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="d0c92-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAirWatch (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c92-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0c92-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d0c92-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0c92-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c92-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c92-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0c92-110">Prerequisites</span></span>

<span data-ttu-id="d0c92-111">tooconfigure integracji z usługą Azure AD z AirWatch należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d0c92-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="d0c92-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c92-113">AirWatch jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d0c92-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0c92-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0c92-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d0c92-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0c92-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d0c92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c92-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c92-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c92-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d0c92-118">Scenario description</span></span>
<span data-ttu-id="d0c92-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d0c92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0c92-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d0c92-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c92-121">Dodawanie AirWatch z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0c92-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="d0c92-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0c92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="d0c92-123">Dodawanie AirWatch z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0c92-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="d0c92-124">tooconfigure hello integracji AirWatch do usługi Azure AD, należy tooadd AirWatch z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0c92-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0c92-125">**tooadd AirWatch z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0c92-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c92-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0c92-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d0c92-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0c92-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d0c92-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d0c92-133">W polu wyszukiwania hello wpisz **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-133">In hello search box, type **AirWatch**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="d0c92-135">W panelu wyników hello zaznacz **AirWatch**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0c92-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0c92-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0c92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0c92-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AirWatch na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d0c92-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0c92-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AirWatch jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c92-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="d0c92-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AirWatch musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d0c92-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="d0c92-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w AirWatch.</span><span class="sxs-lookup"><span data-stu-id="d0c92-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="d0c92-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AirWatch, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d0c92-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0c92-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0c92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0c92-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0c92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0c92-145">**[Tworzenie użytkownika testowego AirWatch](#creating-a-airwatch-test-user)**  -toohave odpowiednikiem Simona Britta w AirWatch, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0c92-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0c92-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0c92-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0c92-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d0c92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0c92-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0c92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0c92-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AirWatch.</span><span class="sxs-lookup"><span data-stu-id="d0c92-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="d0c92-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z AirWatch, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0c92-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c92-151">W portalu Azure na powitania hello **AirWatch** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d0c92-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0c92-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="d0c92-155">Na powitania **AirWatch domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c92-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="d0c92-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0c92-157">a.</span></span> <span data-ttu-id="d0c92-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="d0c92-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="d0c92-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0c92-159">b.</span></span> <span data-ttu-id="d0c92-160">W hello **identyfikator** pole tekstowe, wartość hello typu jako`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="d0c92-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0c92-161">Ta wartość nie jest prawdziwe hello.</span><span class="sxs-lookup"><span data-stu-id="d0c92-161">This value is not hello real.</span></span> <span data-ttu-id="d0c92-162">Zaktualizuj tę wartość przy hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="d0c92-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="d0c92-163">Skontaktuj się z [zespołem pomocy technicznej klienta AirWatch](http://www.air-watch.com/company/contact-us/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d0c92-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="d0c92-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0c92-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="d0c92-166">Na powitania **konfiguracji AirWatch** kliknij **skonfigurować AirWatch** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d0c92-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d0c92-167">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d0c92-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="d0c92-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0c92-169">Click **Save** button.</span></span>

    <span data-ttu-id="d0c92-170">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="d0c92-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="d0c92-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy AirWatch tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d0c92-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="d0c92-172">W okienku nawigacji po lewej stronie powitania kliknij **kont**, a następnie kliknij przycisk **Administratorzy**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="d0c92-173">![Administratorzy](./media/active-directory-saas-airwatch-tutorial/ic791920.png "administratorów")</span><span class="sxs-lookup"><span data-stu-id="d0c92-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="d0c92-174">Rozwiń węzeł hello **ustawienia** menu, a następnie kliknij przycisk **usług katalogowych**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="d0c92-175">![Ustawienia](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="d0c92-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="d0c92-176">Kliknij przycisk hello **użytkownika** na karcie hello **bazowa nazwa Wyróżniająca** tekstowym, wpisz nazwę domeny, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="d0c92-177">![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791922.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d0c92-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="d0c92-178">Kliknij przycisk hello **serwera** kartę.</span><span class="sxs-lookup"><span data-stu-id="d0c92-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="d0c92-179">![Serwer](./media/active-directory-saas-airwatch-tutorial/ic791923.png "serwera")</span><span class="sxs-lookup"><span data-stu-id="d0c92-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="d0c92-180">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c92-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="d0c92-181">![Przekaż](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Przekaż")</span><span class="sxs-lookup"><span data-stu-id="d0c92-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="d0c92-182">a.</span><span class="sxs-lookup"><span data-stu-id="d0c92-182">a.</span></span> <span data-ttu-id="d0c92-183">Jako **typ katalogu**, wybierz pozycję **Brak**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="d0c92-184">b.</span><span class="sxs-lookup"><span data-stu-id="d0c92-184">b.</span></span> <span data-ttu-id="d0c92-185">Wybierz **SAML jest używany do uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="d0c92-186">c.</span><span class="sxs-lookup"><span data-stu-id="d0c92-186">c.</span></span> <span data-ttu-id="d0c92-187">tooupload hello pobranego certyfikatu, kliknij przycisk **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="d0c92-188">W hello **żądania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c92-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="d0c92-189">![Żądanie](./media/active-directory-saas-airwatch-tutorial/ic791925.png "żądania")</span><span class="sxs-lookup"><span data-stu-id="d0c92-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="d0c92-190">a.</span><span class="sxs-lookup"><span data-stu-id="d0c92-190">a.</span></span> <span data-ttu-id="d0c92-191">Jako **żądania typu powiązania**, wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="d0c92-192">b.</span><span class="sxs-lookup"><span data-stu-id="d0c92-192">b.</span></span> <span data-ttu-id="d0c92-193">W portalu Azure na powitania hello **skonfigurować logowanie jednokrotne w Airwatch** strony okna dialogowego, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **dostawcy tożsamości Pojedynczy znak na adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="d0c92-194">c.</span><span class="sxs-lookup"><span data-stu-id="d0c92-194">c.</span></span> <span data-ttu-id="d0c92-195">Jako **NameID Format**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="d0c92-196">d.</span><span class="sxs-lookup"><span data-stu-id="d0c92-196">d.</span></span> <span data-ttu-id="d0c92-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-197">Click **Save**.</span></span>

14. <span data-ttu-id="d0c92-198">Kliknij przycisk hello **użytkownika** karcie ponownie.</span><span class="sxs-lookup"><span data-stu-id="d0c92-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="d0c92-199">![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791926.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d0c92-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="d0c92-200">W hello **atrybutu** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c92-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="d0c92-201">![Atrybut](./media/active-directory-saas-airwatch-tutorial/ic791927.png "atrybutu")</span><span class="sxs-lookup"><span data-stu-id="d0c92-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="d0c92-202">a.</span><span class="sxs-lookup"><span data-stu-id="d0c92-202">a.</span></span> <span data-ttu-id="d0c92-203">W hello **identyfikator obiektu** pole tekstowe, typ **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="d0c92-204">b.</span><span class="sxs-lookup"><span data-stu-id="d0c92-204">b.</span></span> <span data-ttu-id="d0c92-205">W hello **Username** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="d0c92-206">c.</span><span class="sxs-lookup"><span data-stu-id="d0c92-206">c.</span></span> <span data-ttu-id="d0c92-207">W hello **Nazwa wyświetlana** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="d0c92-208">d.</span><span class="sxs-lookup"><span data-stu-id="d0c92-208">d.</span></span> <span data-ttu-id="d0c92-209">W hello **imię** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="d0c92-210">e.</span><span class="sxs-lookup"><span data-stu-id="d0c92-210">e.</span></span> <span data-ttu-id="d0c92-211">W hello **nazwisko** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="d0c92-212">f.</span><span class="sxs-lookup"><span data-stu-id="d0c92-212">f.</span></span> <span data-ttu-id="d0c92-213">W hello **E-mail** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="d0c92-214">g.</span><span class="sxs-lookup"><span data-stu-id="d0c92-214">g.</span></span> <span data-ttu-id="d0c92-215">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0c92-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c92-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0c92-217">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d0c92-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d0c92-219">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0c92-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c92-220">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0c92-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0c92-222">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0c92-224">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0c92-226">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0c92-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0c92-228">a.</span><span class="sxs-lookup"><span data-stu-id="d0c92-228">a.</span></span> <span data-ttu-id="d0c92-229">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c92-230">b.</span><span class="sxs-lookup"><span data-stu-id="d0c92-230">b.</span></span> <span data-ttu-id="d0c92-231">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0c92-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d0c92-232">c.</span><span class="sxs-lookup"><span data-stu-id="d0c92-232">c.</span></span> <span data-ttu-id="d0c92-233">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0c92-234">d.</span><span class="sxs-lookup"><span data-stu-id="d0c92-234">d.</span></span> <span data-ttu-id="d0c92-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="d0c92-236">Tworzenie użytkownika testowego AirWatch</span><span class="sxs-lookup"><span data-stu-id="d0c92-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="d0c92-237">toolog użytkowników tooenable usługi Azure AD w tooAirWatch, muszą mieć przydzielone w tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="d0c92-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="d0c92-238">Gdy AirWatch, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="d0c92-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="d0c92-239">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d0c92-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c92-240">Zaloguj się za tooyour **AirWatch** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d0c92-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="d0c92-241">W okienku nawigacji hello po lewej stronie powitania kliknij **kont**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="d0c92-242">![Użytkownicy](./media/active-directory-saas-airwatch-tutorial/ic791929.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="d0c92-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="d0c92-243">W hello **użytkowników** menu, kliknij przycisk **widok listy**, a następnie kliknij przycisk **Dodaj \> Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="d0c92-244">![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d0c92-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="d0c92-245">Na powitania **Dodaj / Edytuj użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c92-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="d0c92-246">![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d0c92-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="d0c92-247">Typ hello **Username**, **hasło**, **Potwierdź hasło**, **imię**, **nazwisko**,  **Adres e-mail** prawidłowy Azure związanych z kontem usługi Active Directory, mają tooprovision w hello pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d0c92-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="d0c92-248">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="d0c92-249">Możesz użyć innych AirWatch użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AirWatch tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="d0c92-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0c92-250">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c92-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0c92-251">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="d0c92-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d0c92-253">**tooassign tooAirWatch Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d0c92-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c92-254">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d0c92-256">Z listy aplikacji hello wybierz **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-256">In hello applications list, select **AirWatch**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="d0c92-258">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d0c92-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d0c92-260">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0c92-260">Click **Add** button.</span></span> <span data-ttu-id="d0c92-261">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d0c92-263">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0c92-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0c92-264">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0c92-265">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c92-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0c92-266">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0c92-266">Testing single sign-on</span></span>

<span data-ttu-id="d0c92-267">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d0c92-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0c92-268">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d0c92-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d0c92-269">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0c92-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d0c92-270">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d0c92-270">Additional resources</span></span>

* [<span data-ttu-id="d0c92-271">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0c92-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0c92-272">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0c92-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

