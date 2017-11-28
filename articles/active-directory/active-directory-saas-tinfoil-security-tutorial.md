---
title: "Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługę TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="4d04b-103">Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="4d04b-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="4d04b-104">Z tego samouczka, dowiesz się, jak toointegrate usługę TINFOIL SECURITY w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d04b-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d04b-105">Integracja z usługą Azure AD usługę TINFOIL SECURITY zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4d04b-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d04b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTINFOIL zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4d04b-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="4d04b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTINFOIL zabezpieczeń (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d04b-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d04b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4d04b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d04b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d04b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d04b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4d04b-110">Prerequisites</span></span>

<span data-ttu-id="4d04b-111">tooconfigure integracji z usługą Azure AD przy użyciu usługi TINFOIL SECURITY należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4d04b-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="4d04b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d04b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d04b-113">Usługa TINFOIL SECURITY logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4d04b-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d04b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d04b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4d04b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d04b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4d04b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d04b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d04b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d04b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4d04b-118">Scenario description</span></span>
<span data-ttu-id="4d04b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4d04b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d04b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4d04b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d04b-121">Dodaj usługę TINFOIL SECURITY z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4d04b-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="4d04b-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4d04b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="4d04b-123">Dodaj usługę TINFOIL SECURITY z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4d04b-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="4d04b-124">tooconfigure hello integracji usługa TINFOIL SECURITY do usługi Azure AD, należy tooadd usługę TINFOIL SECURITY z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4d04b-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d04b-125">**tooadd usługę TINFOIL SECURITY z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4d04b-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d04b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4d04b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4d04b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d04b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4d04b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4d04b-133">W polu wyszukiwania hello wpisz **usługę TINFOIL SECURITY**, wybierz pozycję **usługę TINFOIL SECURITY** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4d04b-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Usługa TINFOIL SECURITY z galerii](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4d04b-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4d04b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4d04b-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługę TINFOIL SECURITY w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d04b-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługę TINFOIL SECURITY jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d04b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="4d04b-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługę TINFOIL SECURITY musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4d04b-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="4d04b-139">Usługa TINFOIL SECURITY przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="4d04b-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d04b-140">tooconfigure i testowych usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4d04b-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d04b-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4d04b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d04b-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4d04b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d04b-143">**[Tworzenie użytkownika testowego usługę TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave odpowiednikiem Simona Britta w usługę TINFOIL SECURITY, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d04b-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d04b-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4d04b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d04b-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4d04b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4d04b-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4d04b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4d04b-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="4d04b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="4d04b-148">**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4d04b-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d04b-149">W portalu Azure na powitania hello **usługę TINFOIL SECURITY** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4d04b-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4d04b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML na podstawie logowania jednokrotnego](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="4d04b-153">Na powitania **TINFOIL SECURITY domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04b-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="4d04b-155">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość.</span><span class="sxs-lookup"><span data-stu-id="4d04b-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="4d04b-157">Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d04b-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="4d04b-158">![Atrybuty](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="4d04b-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="4d04b-159">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="4d04b-159">Attribute Name</span></span>    |   <span data-ttu-id="4d04b-160">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="4d04b-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="4d04b-161">AccountID</span><span class="sxs-lookup"><span data-stu-id="4d04b-161">accountid</span></span> | <span data-ttu-id="4d04b-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="4d04b-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="4d04b-163">a.</span><span class="sxs-lookup"><span data-stu-id="4d04b-163">a.</span></span> <span data-ttu-id="4d04b-164">Kliknij przycisk **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="4d04b-165">![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="4d04b-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="4d04b-166">![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="4d04b-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="4d04b-167">b.</span><span class="sxs-lookup"><span data-stu-id="4d04b-167">b.</span></span> <span data-ttu-id="4d04b-168">W hello **nazwa atrybutu** pole tekstowe, typ **accountid**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="4d04b-169">c.</span><span class="sxs-lookup"><span data-stu-id="4d04b-169">c.</span></span> <span data-ttu-id="4d04b-170">W hello **wartość atrybutu** pole tekstowe, Wklej hello konta identyfikator wartość, która zostanie wyświetlony później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="4d04b-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="4d04b-171">d.</span><span class="sxs-lookup"><span data-stu-id="4d04b-171">d.</span></span> <span data-ttu-id="4d04b-172">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="4d04b-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4d04b-173">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4d04b-175">Na powitania **TINFOIL SECURITY Configuration** kliknij **skonfigurować usługę TINFOIL SECURITY** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4d04b-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d04b-176">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4d04b-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja zabezpieczeń TINFOIL](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="4d04b-178">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy usługę TINFOIL SECURITY jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4d04b-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="4d04b-179">Witaj pasku narzędzi u góry hello, kliknij przycisk **Moje konto**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="4d04b-180">![Pulpit nawigacyjny](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "pulpitu nawigacyjnego")</span><span class="sxs-lookup"><span data-stu-id="4d04b-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="4d04b-181">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-181">Click **Security**.</span></span>
   
    <span data-ttu-id="4d04b-182">![Zabezpieczenia](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="4d04b-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="4d04b-183">Na powitania **rejestracji jednokrotnej** konfiguracji wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d04b-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4d04b-184">![Logowanie jednokrotne](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="4d04b-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="4d04b-185">a.</span><span class="sxs-lookup"><span data-stu-id="4d04b-185">a.</span></span> <span data-ttu-id="4d04b-186">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="4d04b-187">b.</span><span class="sxs-lookup"><span data-stu-id="4d04b-187">b.</span></span> <span data-ttu-id="4d04b-188">Kliknij przycisk **ręcznej konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="4d04b-189">c.</span><span class="sxs-lookup"><span data-stu-id="4d04b-189">c.</span></span> <span data-ttu-id="4d04b-190">W **adresu URL przesyłania SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4d04b-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="4d04b-191">d.</span><span class="sxs-lookup"><span data-stu-id="4d04b-191">d.</span></span> <span data-ttu-id="4d04b-192">W **odcisk palca certyfikatu SAML** pole tekstowe, Wklej wartość hello **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d04b-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="4d04b-193">e.</span><span class="sxs-lookup"><span data-stu-id="4d04b-193">e.</span></span> <span data-ttu-id="4d04b-194">Kopiuj **swój identyfikator konta** i Wklej wartość hello w **wartość atrybutu** pole tekstowe, w obszarze **Dodawanie atrybutu** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4d04b-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="4d04b-195">f.</span><span class="sxs-lookup"><span data-stu-id="4d04b-195">f.</span></span> <span data-ttu-id="4d04b-196">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4d04b-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4d04b-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d04b-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4d04b-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d04b-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d04b-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4d04b-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d04b-200">Create an Azure AD test user</span></span>
<span data-ttu-id="4d04b-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4d04b-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4d04b-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4d04b-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d04b-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4d04b-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d04b-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="4d04b-207">Użytkownicy i grupy -> Wszyscy użytkownicy</span><span class="sxs-lookup"><span data-stu-id="4d04b-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d04b-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Użytkownik](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d04b-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4d04b-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d04b-212">a.</span><span class="sxs-lookup"><span data-stu-id="4d04b-212">a.</span></span> <span data-ttu-id="4d04b-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d04b-214">b.</span><span class="sxs-lookup"><span data-stu-id="4d04b-214">b.</span></span> <span data-ttu-id="4d04b-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4d04b-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d04b-216">c.</span><span class="sxs-lookup"><span data-stu-id="4d04b-216">c.</span></span> <span data-ttu-id="4d04b-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d04b-218">d.</span><span class="sxs-lookup"><span data-stu-id="4d04b-218">d.</span></span> <span data-ttu-id="4d04b-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="4d04b-220">Tworzenie użytkownika testowego usługę TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="4d04b-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="4d04b-221">W kolejności tooenable usługi Azure AD użytkownicy toolog do usługę TINFOIL SECURITY musi być przygotowana do usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="4d04b-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="4d04b-222">W przypadku hello usługę TINFOIL SECURITY Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="4d04b-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="4d04b-223">**tooget użytkownika zainicjowano obsługę administracyjną, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4d04b-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d04b-224">Jeśli użytkownik hello jest część konta organizacji, należy za[skontaktuj się z zespołem pomocy technicznej usługę TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) tooget hello konta konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d04b-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="4d04b-225">Jeśli użytkownik hello jest zwykłych użytkowników TINFOIL SECURITY SaaS, hello użytkownik może dodać tooany współpracownika witryn hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d04b-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="4d04b-226">Ta usługa wyzwalaczy toosend procesu, określony toohello zaproszenia poczty e-mail toocreate nowego konta użytkownika usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="4d04b-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="4d04b-227">Możesz użyć innych usługę TINFOIL SECURITY użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez usługę TINFOIL SECURITY tooprovision konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d04b-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4d04b-228">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d04b-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4d04b-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTINFOIL zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4d04b-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4d04b-231">**tooassign tooTINFOIL Simona Britta zabezpieczeń, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4d04b-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d04b-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4d04b-234">Z listy aplikacji hello wybierz **usługę TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![Wybierz usługę TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="4d04b-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4d04b-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4d04b-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4d04b-238">Click **Add** button.</span></span> <span data-ttu-id="4d04b-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4d04b-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4d04b-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d04b-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d04b-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4d04b-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4d04b-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4d04b-244">Test single sign-on</span></span>

<span data-ttu-id="4d04b-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4d04b-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4d04b-246">Po kliknięciu kafelka usługę TINFOIL SECURITY hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour usługę TINFOIL SECURITY aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4d04b-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="4d04b-247">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d04b-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d04b-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4d04b-248">Additional resources</span></span>

* [<span data-ttu-id="4d04b-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d04b-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d04b-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d04b-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

