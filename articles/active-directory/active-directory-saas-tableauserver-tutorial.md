---
title: "Samouczek: Azure Active Directory integrację z serwerem Tableau | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i serwera Tableau."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="bf7aa-103">Samouczek: Azure Active Directory integrację z serwerem Tableau</span><span class="sxs-lookup"><span data-stu-id="bf7aa-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="bf7aa-104">Z tego samouczka dowiesz się integrowanie Tableau serwera z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf7aa-105">Integrowanie Tableau serwera z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf7aa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do serwera Tableau</span><span class="sxs-lookup"><span data-stu-id="bf7aa-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="bf7aa-107">Umożliwia użytkownikom automatycznie pobrać zalogowane serwerowi Tableau (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf7aa-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf7aa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bf7aa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf7aa-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf7aa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bf7aa-110">Prerequisites</span></span>

<span data-ttu-id="bf7aa-111">Aby skonfigurować integrację usługi Azure AD z serwerem Tableau, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="bf7aa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf7aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf7aa-113">Serwer Tableau logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bf7aa-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf7aa-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf7aa-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf7aa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf7aa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf7aa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bf7aa-118">Scenario description</span></span>
<span data-ttu-id="bf7aa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf7aa-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf7aa-121">Dodanie serwera Tableau z galerii</span><span class="sxs-lookup"><span data-stu-id="bf7aa-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="bf7aa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf7aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="bf7aa-123">Dodanie serwera Tableau z galerii</span><span class="sxs-lookup"><span data-stu-id="bf7aa-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="bf7aa-124">Aby skonfigurować integrację serwera Tableau do usługi Azure AD, należy dodać serwer Tableau z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf7aa-125">**Aby dodać serwer Tableau z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf7aa-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7aa-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bf7aa-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf7aa-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bf7aa-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bf7aa-133">W polu wyszukiwania wpisz **serwera Tableau**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-133">In the search box, type **Tableau Server**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="bf7aa-135">W panelu wyników wybierz **serwera Tableau**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf7aa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf7aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf7aa-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z serwerem Tableau oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bf7aa-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf7aa-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Tableau serwera jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="bf7aa-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi na serwerze Tableau musi określone.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="bf7aa-141">Na serwerze Tableau, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf7aa-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z serwerem Tableau, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf7aa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf7aa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf7aa-145">**[Tworzenie użytkownika testowego serwera Tableau](#creating-a-tableau-server-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Tableau serwera, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf7aa-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf7aa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf7aa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf7aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf7aa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="bf7aa-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z serwerem Tableau, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf7aa-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7aa-151">W portalu Azure na **serwera Tableau** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bf7aa-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="bf7aa-155">Na **adresy URL i domeną serwera Tableau** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="bf7aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-157">a.</span></span> <span data-ttu-id="bf7aa-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="bf7aa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="bf7aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-159">b.</span></span> <span data-ttu-id="bf7aa-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="bf7aa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="bf7aa-161">c.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-161">c.</span></span> <span data-ttu-id="bf7aa-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="bf7aa-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bf7aa-163">Poprzednie wartości nie są wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-163">The preceding values are not real values.</span></span> <span data-ttu-id="bf7aa-164">Później należy zaktualizować wartości z rzeczywistego adresu URL i identyfikator ze strony konfiguracji serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="bf7aa-165">Aplikacja serwera TABLEAU oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bf7aa-166">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-166">Configure the following claims for this application.</span></span> <span data-ttu-id="bf7aa-167">Możesz zarządzać wartości tych atrybutów z **"Atrybuty użytkownika"** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="bf7aa-168">Poniższy zrzut ekranu przedstawia przykład dla tego samego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-168">The following screenshot shows an example for the same.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="bf7aa-170">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="bf7aa-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="bf7aa-171">Attribute Name</span></span> | <span data-ttu-id="bf7aa-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="bf7aa-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="bf7aa-173">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="bf7aa-173">username</span></span> | <span data-ttu-id="bf7aa-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="bf7aa-174">*user.displayname*</span></span> |

    <span data-ttu-id="bf7aa-175">a.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-175">a.</span></span> <span data-ttu-id="bf7aa-176">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="bf7aa-179">b.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-179">b.</span></span> <span data-ttu-id="bf7aa-180">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bf7aa-181">c.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-181">c.</span></span> <span data-ttu-id="bf7aa-182">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bf7aa-183">d.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-183">d.</span></span> <span data-ttu-id="bf7aa-184">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="bf7aa-184">Click **Ok**</span></span>


6. <span data-ttu-id="bf7aa-185">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="bf7aa-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-187">Click **Save** button.</span></span>

    <span data-ttu-id="bf7aa-188">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="bf7aa-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="bf7aa-189">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, musisz logowanie do serwera Tableau dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="bf7aa-190">a.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-190">a.</span></span> <span data-ttu-id="bf7aa-191">W konfiguracji serwera Tableau, kliknij przycisk **SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="bf7aa-193">b.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-193">b.</span></span> <span data-ttu-id="bf7aa-194">Zaznacz pole wyboru z **SAML używana dla logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="bf7aa-195">c.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-195">c.</span></span> <span data-ttu-id="bf7aa-196">Serwer TABLEAU adres zwrotny URL — adres URL, który serwer Tableau użytkownicy będą uzyskiwać dostęp do, takich jak http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="bf7aa-197">Nie zaleca się przy użyciu http://localhost.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="bf7aa-198">Przy użyciu adresu URL znakiem ukośnika (na przykład http://tableau_server/) nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="bf7aa-199">Kopia **serwera Tableau zwrotnego adresu URL** i wklej go do usługi Azure AD **na adres URL logowania** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="bf7aa-200">d.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-200">d.</span></span> <span data-ttu-id="bf7aa-201">Identyfikator jednostki SAML — identyfikator jednostki jednoznacznie identyfikuje instalacją serwera Tableau do dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="bf7aa-202">Możesz wprowadzić adres URL serwera Tableau ponownie, jeśli chcesz, ale nie musi być adres URL serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="bf7aa-203">Kopiuj **SAML identyfikator jednostki** i wklej go do usługi Azure AD **identyfikator** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="bf7aa-204">e.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-204">e.</span></span> <span data-ttu-id="bf7aa-205">Kliknij przycisk **Eksportuj plik metadanych** i otwórz go w aplikacji, Edytor tekstu.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="bf7aa-206">Znajdź adres URL usługi klienta potwierdzenia z Http Post i indeksu 0 i skopiuj adres URL.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="bf7aa-207">Teraz wklej go do usługi Azure AD **adres URL odpowiedzi** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="bf7aa-208">f.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-208">f.</span></span> <span data-ttu-id="bf7aa-209">Zlokalizuj plik metadanych Federacji pobrany z portalu Azure, a następnie przekaż go w **pliku metadanych SAML Idp**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="bf7aa-210">g.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-210">g.</span></span> <span data-ttu-id="bf7aa-211">Kliknij przycisk **OK** przycisku na stronie Konfiguracja serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="bf7aa-212">Trzeba przekazać dowolny certyfikat w konfiguracji logowania jednokrotnego SAML serwera Tableau i zostaną uzyskać pominięte w procesie logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="bf7aa-213">Jeśli konieczne pomoc w konfigurowaniu SAML na serwerze Tableau, można znaleźć w tym artykule [skonfigurować SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="bf7aa-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bf7aa-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf7aa-215">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf7aa-216">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf7aa-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf7aa-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf7aa-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf7aa-218">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bf7aa-220">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf7aa-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7aa-221">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf7aa-223">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf7aa-225">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf7aa-227">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf7aa-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf7aa-229">a.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-229">a.</span></span> <span data-ttu-id="bf7aa-230">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf7aa-231">b.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-231">b.</span></span> <span data-ttu-id="bf7aa-232">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf7aa-233">c.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-233">c.</span></span> <span data-ttu-id="bf7aa-234">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf7aa-235">d.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-235">d.</span></span> <span data-ttu-id="bf7aa-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="bf7aa-237">Tworzenie użytkownika testowego Tableau serwera</span><span class="sxs-lookup"><span data-stu-id="bf7aa-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="bf7aa-238">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Tableau serwera.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="bf7aa-239">Należy udostępnić wszystkich użytkowników na serwerze Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="bf7aa-240">Że nazwa użytkownika powinna być zgodna wartość, które zostały skonfigurowane w atrybucie niestandardowym usługi Azure AD z **username**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="bf7aa-241">Z mapowaniem poprawną integrację powinny działać [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="bf7aa-242">Należy ręcznie utworzyć użytkownika, należy skontaktować się z administratorem serwera Tableau w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf7aa-243">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf7aa-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf7aa-244">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bf7aa-246">**Aby przypisać Simona Britta Tableau serwera, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf7aa-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="bf7aa-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bf7aa-249">Na liście aplikacji zaznacz **serwera Tableau**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-249">In the applications list, select **Tableau Server**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="bf7aa-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bf7aa-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-253">Click **Add** button.</span></span> <span data-ttu-id="bf7aa-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bf7aa-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf7aa-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf7aa-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf7aa-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf7aa-259">Testing single sign-on</span></span>

<span data-ttu-id="bf7aa-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf7aa-261">Po kliknięciu kafelka Tableau serwera w panelu dostępu należy powinien pobrać automatycznie podpisany w przypadku aplikacji serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="bf7aa-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="bf7aa-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bf7aa-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bf7aa-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bf7aa-263">Additional resources</span></span>

* [<span data-ttu-id="bf7aa-264">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf7aa-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf7aa-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf7aa-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

