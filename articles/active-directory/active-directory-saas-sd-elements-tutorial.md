---
title: 'Samouczek: Integracji Azure Active Directory z elementami SD | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i elementy SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="ebc95-103">Samouczek: Integracji Azure Active Directory z elementami SD.</span><span class="sxs-lookup"><span data-stu-id="ebc95-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="ebc95-104">Z tego samouczka, dowiesz się, jak toointegrate SD elementów w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebc95-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebc95-105">Integrowanie SD elementy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ebc95-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebc95-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSD elementów</span><span class="sxs-lookup"><span data-stu-id="ebc95-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="ebc95-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSD elementy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc95-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebc95-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ebc95-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ebc95-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebc95-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebc95-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ebc95-110">Prerequisites</span></span>

<span data-ttu-id="ebc95-111">tooconfigure integracji usługi Azure AD z elementami SD, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ebc95-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="ebc95-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc95-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebc95-113">Elementy SD logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ebc95-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebc95-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebc95-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ebc95-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebc95-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ebc95-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebc95-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebc95-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebc95-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ebc95-118">Scenario description</span></span>
<span data-ttu-id="ebc95-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ebc95-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebc95-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ebc95-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebc95-121">Dodawanie elementów SD z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ebc95-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="ebc95-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ebc95-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="ebc95-123">Dodawanie elementów SD z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ebc95-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="ebc95-124">tooconfigure hello integracji SD elementów do usługi Azure AD, należy tooadd SD elementy z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ebc95-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebc95-125">**tooadd SD elementów z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ebc95-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc95-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ebc95-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ebc95-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebc95-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ebc95-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ebc95-133">W polu wyszukiwania hello wpisz **elementy SD**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-133">In hello search box, type **SD Elements**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="ebc95-135">W panelu wyników hello, wybierz **elementy SD**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ebc95-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebc95-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ebc95-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebc95-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z elementami SD, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebc95-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w elementach SD jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebc95-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="ebc95-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w elementach SD musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ebc95-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="ebc95-141">W elementach SD, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ebc95-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebc95-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z elementami SD, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ebc95-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebc95-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebc95-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebc95-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ebc95-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebc95-145">**[Tworzenie użytkownika testowego elementy SD](#creating-a-sd-elements-test-user)**  -toohave odpowiednikiem Simona Britta w elementach SD, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ebc95-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebc95-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ebc95-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebc95-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ebc95-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebc95-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ebc95-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebc95-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji SD elementów.</span><span class="sxs-lookup"><span data-stu-id="ebc95-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="ebc95-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z elementami SD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ebc95-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc95-151">W portalu Azure na powitania hello **elementy SD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ebc95-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ebc95-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="ebc95-155">Na powitania **SD elementy domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ebc95-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="ebc95-157">a.</span><span class="sxs-lookup"><span data-stu-id="ebc95-157">a.</span></span> <span data-ttu-id="ebc95-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="ebc95-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="ebc95-159">b.</span><span class="sxs-lookup"><span data-stu-id="ebc95-159">b.</span></span> <span data-ttu-id="ebc95-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="ebc95-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ebc95-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ebc95-161">These values are not real.</span></span> <span data-ttu-id="ebc95-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ebc95-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ebc95-163">Skontaktuj się z [elementy SD obsługują zespołu](mailto:support@sdelements.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ebc95-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="ebc95-164">Elementy SD aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="ebc95-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ebc95-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebc95-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ebc95-166">Można zarządzać hello wartości tych atrybutów z hello **"Użytkownika atrybutu"** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ebc95-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="ebc95-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-167">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="ebc95-169">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ebc95-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="ebc95-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="ebc95-170">Attribute Name</span></span> | <span data-ttu-id="ebc95-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="ebc95-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ebc95-172">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="ebc95-172">email</span></span> |<span data-ttu-id="ebc95-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="ebc95-173">user.mail</span></span> |
    | <span data-ttu-id="ebc95-174">Imię</span><span class="sxs-lookup"><span data-stu-id="ebc95-174">firstname</span></span> |<span data-ttu-id="ebc95-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ebc95-175">user.givenname</span></span> |
    | <span data-ttu-id="ebc95-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="ebc95-176">lastname</span></span> |<span data-ttu-id="ebc95-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="ebc95-177">user.surname</span></span> |

    <span data-ttu-id="ebc95-178">a.</span><span class="sxs-lookup"><span data-stu-id="ebc95-178">a.</span></span> <span data-ttu-id="ebc95-179">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="ebc95-182">b.</span><span class="sxs-lookup"><span data-stu-id="ebc95-182">b.</span></span> <span data-ttu-id="ebc95-183">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ebc95-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ebc95-184">c.</span><span class="sxs-lookup"><span data-stu-id="ebc95-184">c.</span></span> <span data-ttu-id="ebc95-185">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ebc95-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ebc95-186">d.</span><span class="sxs-lookup"><span data-stu-id="ebc95-186">d.</span></span> <span data-ttu-id="ebc95-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="ebc95-188">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ebc95-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="ebc95-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ebc95-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ebc95-192">Na powitania **SD elementy konfiguracji** kliknij **skonfigurować elementy SD** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ebc95-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebc95-193">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ebc95-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="ebc95-195">tooget logowanie jednokrotne włączone, skontaktuj się z Twojego [elementy SD obsługują zespołu](mailto:support@sdelements.com) i dostarczać hello pliku pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ebc95-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="ebc95-196">W oknie innej przeglądarki, tooyour logowania jednokrotnego elementy SD dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="ebc95-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="ebc95-197">W menu hello na górze hello, kliknij przycisk **systemu**, a następnie **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="ebc95-199">Na powitania **ustawień rejestracji jednokrotnej** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ebc95-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="ebc95-201">a.</span><span class="sxs-lookup"><span data-stu-id="ebc95-201">a.</span></span> <span data-ttu-id="ebc95-202">Jako **typ logowania jednokrotnego**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="ebc95-203">b.</span><span class="sxs-lookup"><span data-stu-id="ebc95-203">b.</span></span> <span data-ttu-id="ebc95-204">W hello **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc95-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="ebc95-205">c.</span><span class="sxs-lookup"><span data-stu-id="ebc95-205">c.</span></span> <span data-ttu-id="ebc95-206">W hello **Dostawca pojedynczego logowania jednokrotnego usługi tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc95-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="ebc95-207">d.</span><span class="sxs-lookup"><span data-stu-id="ebc95-207">d.</span></span> <span data-ttu-id="ebc95-208">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ebc95-209">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ebc95-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebc95-210">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ebc95-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebc95-211">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebc95-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebc95-212">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc95-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebc95-213">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ebc95-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ebc95-215">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ebc95-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc95-216">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ebc95-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebc95-218">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebc95-220">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebc95-222">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ebc95-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebc95-224">a.</span><span class="sxs-lookup"><span data-stu-id="ebc95-224">a.</span></span> <span data-ttu-id="ebc95-225">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebc95-226">b.</span><span class="sxs-lookup"><span data-stu-id="ebc95-226">b.</span></span> <span data-ttu-id="ebc95-227">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ebc95-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebc95-228">c.</span><span class="sxs-lookup"><span data-stu-id="ebc95-228">c.</span></span> <span data-ttu-id="ebc95-229">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ebc95-230">d.</span><span class="sxs-lookup"><span data-stu-id="ebc95-230">d.</span></span> <span data-ttu-id="ebc95-231">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="ebc95-232">Tworzenie użytkownika testowego elementy SD.</span><span class="sxs-lookup"><span data-stu-id="ebc95-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="ebc95-233">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta SD elementów.</span><span class="sxs-lookup"><span data-stu-id="ebc95-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="ebc95-234">W przypadku hello elementy SD tworzenie elementów SD użytkowników jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ebc95-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="ebc95-235">**toocreate Simona Britta w elementach SD, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ebc95-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc95-236">W oknie przeglądarki sieci web, witryny firmy elementy SD tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ebc95-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="ebc95-237">W menu hello na górze hello, kliknij przycisk **Zarządzanie użytkownikami**, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="ebc95-239">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-239">Click **Add New User**.</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="ebc95-241">Na powitania **Dodaj nowego użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ebc95-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="ebc95-243">a.</span><span class="sxs-lookup"><span data-stu-id="ebc95-243">a.</span></span> <span data-ttu-id="ebc95-244">W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ebc95-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="ebc95-245">b.</span><span class="sxs-lookup"><span data-stu-id="ebc95-245">b.</span></span> <span data-ttu-id="ebc95-246">W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="ebc95-247">c.</span><span class="sxs-lookup"><span data-stu-id="ebc95-247">c.</span></span> <span data-ttu-id="ebc95-248">W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="ebc95-249">d.</span><span class="sxs-lookup"><span data-stu-id="ebc95-249">d.</span></span> <span data-ttu-id="ebc95-250">Jako **roli**, wybierz pozycję **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="ebc95-251">e.</span><span class="sxs-lookup"><span data-stu-id="ebc95-251">e.</span></span> <span data-ttu-id="ebc95-252">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ebc95-253">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc95-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ebc95-254">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSD elementów.</span><span class="sxs-lookup"><span data-stu-id="ebc95-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ebc95-256">**tooassign Simona Britta tooSD elementów, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ebc95-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc95-257">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ebc95-259">Z listy aplikacji hello wybierz **elementy SD**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-259">In hello applications list, select **SD Elements**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="ebc95-261">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ebc95-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ebc95-263">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ebc95-263">Click **Add** button.</span></span> <span data-ttu-id="ebc95-264">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ebc95-266">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ebc95-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebc95-267">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebc95-268">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ebc95-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebc95-269">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ebc95-269">Testing single sign-on</span></span>

<span data-ttu-id="ebc95-270">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ebc95-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="ebc95-271">Po kliknięciu powitalne elementy SD kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SD elementy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebc95-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebc95-272">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ebc95-272">Additional resources</span></span>

* [<span data-ttu-id="ebc95-273">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebc95-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebc95-274">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ebc95-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

