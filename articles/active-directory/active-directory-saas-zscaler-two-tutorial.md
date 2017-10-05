---
title: "Samouczek: Integracji Azure Active Directory z dwóch Zscaler | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zscaler dwa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 38c9da0a6599bb66c452fdb8a8911338601155f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="24f7c-103">Samouczek: Integracji Azure Active Directory z dwóch Zscaler</span><span class="sxs-lookup"><span data-stu-id="24f7c-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="24f7c-104">Z tego samouczka dowiesz się integrowanie Zscaler dwa z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24f7c-104">In this tutorial, you learn how to integrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24f7c-105">Integrowanie Zscaler dwa z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="24f7c-105">Integrating Zscaler Two with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="24f7c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do dwóch Zscaler</span><span class="sxs-lookup"><span data-stu-id="24f7c-106">You can control in Azure AD who has access to Zscaler Two</span></span>
- <span data-ttu-id="24f7c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do dwóch Zscaler (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24f7c-107">You can enable your users to automatically get signed-on to Zscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24f7c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="24f7c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="24f7c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24f7c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24f7c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24f7c-110">Prerequisites</span></span>

<span data-ttu-id="24f7c-111">Aby skonfigurować integrację usługi Azure AD z dwóch Zscaler, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="24f7c-111">To configure Azure AD integration with Zscaler Two, you need the following items:</span></span>

- <span data-ttu-id="24f7c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24f7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24f7c-113">Dwa Zscaler logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="24f7c-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24f7c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24f7c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="24f7c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24f7c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="24f7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24f7c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24f7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24f7c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="24f7c-118">Scenario description</span></span>
<span data-ttu-id="24f7c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="24f7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24f7c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="24f7c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24f7c-121">Dodawanie dwóch Zscaler z galerii</span><span class="sxs-lookup"><span data-stu-id="24f7c-121">Adding Zscaler Two from the gallery</span></span>
2. <span data-ttu-id="24f7c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="24f7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-the-gallery"></a><span data-ttu-id="24f7c-123">Dodawanie dwóch Zscaler z galerii</span><span class="sxs-lookup"><span data-stu-id="24f7c-123">Adding Zscaler Two from the gallery</span></span>
<span data-ttu-id="24f7c-124">Aby skonfigurować integrację z dwóch Zscaler do usługi Azure AD, należy dodać do listy zarządzane aplikacje SaaS Zscaler dwa z galerii.</span><span class="sxs-lookup"><span data-stu-id="24f7c-124">To configure the integration of Zscaler Two into Azure AD, you need to add Zscaler Two from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24f7c-125">**Aby dodać Zscaler dwa z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24f7c-125">**To add Zscaler Two from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24f7c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="24f7c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="24f7c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="24f7c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="24f7c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="24f7c-133">W polu wyszukiwania wpisz **Zscaler dwóch**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-133">In the search box, type **Zscaler Two**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="24f7c-135">W panelu wyników wybierz **Zscaler dwóch**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="24f7c-135">In the results panel, select **Zscaler Two**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24f7c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="24f7c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24f7c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z dwóch Zscaler w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24f7c-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w drugiej Zscaler do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24f7c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Two is to a user in Azure AD.</span></span> <span data-ttu-id="24f7c-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w dwóch Zscaler musi się.</span><span class="sxs-lookup"><span data-stu-id="24f7c-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Two needs to be established.</span></span>

<span data-ttu-id="24f7c-141">W dwóch Zscaler przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="24f7c-141">In Zscaler Two, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="24f7c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z dwóch Zscaler, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="24f7c-142">To configure and test Azure AD single sign-on with Zscaler Two, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24f7c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="24f7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="24f7c-144">**[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings)**  — Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="24f7c-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="24f7c-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24f7c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="24f7c-146">**[Tworzenie użytkownika testowego dwóch Zscaler](#creating-a-zscaler-two-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Zscaler dwóch połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24f7c-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - to have a counterpart of Britta Simon in Zscaler Two that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="24f7c-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="24f7c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="24f7c-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="24f7c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24f7c-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24f7c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24f7c-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w dwóch Zscaler aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24f7c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="24f7c-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z dwóch Zscaler, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24f7c-151">**To configure Azure AD single sign-on with Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="24f7c-152">W portalu Azure na **Zscaler dwóch** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-152">In the Azure portal, on the **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="24f7c-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="24f7c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="24f7c-156">Na **Zscaler dwie domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-156">On the **Zscaler Two Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="24f7c-158">W polu tekstowym adres URL logowania wpisz adres URL używany przez użytkowników do logowania się na dwóch ZScaler aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24f7c-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24f7c-159">Należy zaktualizować tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="24f7c-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="24f7c-160">Skontaktuj się z [zespołem pomocy technicznej klienta dwóch Zscaler](https://www.zscaler.com/company/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="24f7c-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="24f7c-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="24f7c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="24f7c-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24f7c-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24f7c-165">Na **konfiguracji dwóch Zscaler** , kliknij przycisk **skonfigurować dwa Zscaler** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="24f7c-165">On the **Zscaler Two Configuration** section, click **Configure Zscaler Two** to open **Configure sign-on** window.</span></span> <span data-ttu-id="24f7c-166">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="24f7c-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="24f7c-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do dwóch ZScaler witryny firmy.</span><span class="sxs-lookup"><span data-stu-id="24f7c-168">In a different web browser window, log in to your ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="24f7c-169">W menu u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="24f7c-170">![Administracja](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="24f7c-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="24f7c-171">W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="24f7c-172">![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="24f7c-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="24f7c-173">W **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="24f7c-174">![Uwierzytelnianie](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="24f7c-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="24f7c-175">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-175">a.</span></span> <span data-ttu-id="24f7c-176">Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="24f7c-177">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-177">b.</span></span> <span data-ttu-id="24f7c-178">Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="24f7c-179">Na **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące czynności, a następnie kliknij **gotowe**</span><span class="sxs-lookup"><span data-stu-id="24f7c-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="24f7c-180">![Logowanie jednokrotne](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="24f7c-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="24f7c-181">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-181">a.</span></span> <span data-ttu-id="24f7c-182">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **adres URL portalu SAML, do którego użytkownicy są wysyłane do uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="24f7c-183">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-183">b.</span></span> <span data-ttu-id="24f7c-184">W **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="24f7c-185">c.</span><span class="sxs-lookup"><span data-stu-id="24f7c-185">c.</span></span> <span data-ttu-id="24f7c-186">Aby przekazać certyfikat pobrany, kliknij przycisk **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="24f7c-187">d.</span><span class="sxs-lookup"><span data-stu-id="24f7c-187">d.</span></span> <span data-ttu-id="24f7c-188">Wybierz **Włącz SAML automatycznego inicjowania obsługi**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="24f7c-189">Na **skonfigurować uwierzytelnianie użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="24f7c-190">![Administracja](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="24f7c-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="24f7c-191">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-191">a.</span></span> <span data-ttu-id="24f7c-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-192">Click **Save**.</span></span>

    <span data-ttu-id="24f7c-193">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-193">b.</span></span> <span data-ttu-id="24f7c-194">Kliknij przycisk **Aktywuj teraz**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="24f7c-195">Konfigurowanie ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="24f7c-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="24f7c-196">Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="24f7c-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="24f7c-197">Uruchom **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="24f7c-198">Wybierz **Opcje internetowe** z **narzędzia** menu otwartego **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="24f7c-199">![Opcje internetowe](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Opcje internetowe")</span><span class="sxs-lookup"><span data-stu-id="24f7c-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="24f7c-200">Kliknij przycisk **połączeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="24f7c-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="24f7c-201">![Połączenia](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "połączeń")</span><span class="sxs-lookup"><span data-stu-id="24f7c-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="24f7c-202">Kliknij przycisk **ustawienia sieci LAN** otworzyć **ustawienia sieci LAN** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="24f7c-203">W sekcji serwer Proxy wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="24f7c-204">![Serwer proxy](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "serwera Proxy")</span><span class="sxs-lookup"><span data-stu-id="24f7c-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="24f7c-205">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-205">a.</span></span> <span data-ttu-id="24f7c-206">Wybierz **Użyj serwera proxy dla sieci LAN**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="24f7c-207">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-207">b.</span></span> <span data-ttu-id="24f7c-208">W polu tekstowym adres typu **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-208">In the Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="24f7c-209">c.</span><span class="sxs-lookup"><span data-stu-id="24f7c-209">c.</span></span> <span data-ttu-id="24f7c-210">W polu tekstowym portu, wpisz **80**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="24f7c-211">d.</span><span class="sxs-lookup"><span data-stu-id="24f7c-211">d.</span></span> <span data-ttu-id="24f7c-212">Wybierz **używaj serwera proxy dla adresów lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="24f7c-213">e.</span><span class="sxs-lookup"><span data-stu-id="24f7c-213">e.</span></span> <span data-ttu-id="24f7c-214">Kliknij przycisk **OK** zamknąć **ustawienia sieci lokalnej (LAN)** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="24f7c-215">Kliknij przycisk **OK** zamknąć **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="24f7c-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="24f7c-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="24f7c-217">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="24f7c-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="24f7c-218">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24f7c-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24f7c-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24f7c-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="24f7c-220">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24f7c-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="24f7c-222">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24f7c-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24f7c-223">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="24f7c-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24f7c-225">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24f7c-227">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24f7c-229">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24f7c-231">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-231">a.</span></span> <span data-ttu-id="24f7c-232">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24f7c-233">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-233">b.</span></span> <span data-ttu-id="24f7c-234">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24f7c-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24f7c-235">c.</span><span class="sxs-lookup"><span data-stu-id="24f7c-235">c.</span></span> <span data-ttu-id="24f7c-236">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="24f7c-237">d.</span><span class="sxs-lookup"><span data-stu-id="24f7c-237">d.</span></span> <span data-ttu-id="24f7c-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="24f7c-239">Utworzenie dwóch Zscaler użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="24f7c-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="24f7c-240">Aby umożliwić użytkownikom usługi Azure AD do logowania się dwóch ZScaler, muszą mieć przydzielone do dwóch ZScaler.</span><span class="sxs-lookup"><span data-stu-id="24f7c-240">To enable Azure AD users to log in to ZScaler Two, they must be provisioned to ZScaler Two.</span></span> <span data-ttu-id="24f7c-241">W przypadku dwóch ZScaler Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="24f7c-241">In the case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="24f7c-242">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="24f7c-243">Zaloguj się do Twojego **Zscaler dwóch** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="24f7c-243">Log in to your **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="24f7c-244">Kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="24f7c-245">![Administracja](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="24f7c-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="24f7c-246">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="24f7c-247">![Dodaj](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="24f7c-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="24f7c-248">W **użytkowników** , kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="24f7c-249">![Dodaj](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="24f7c-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="24f7c-250">W sekcji Dodaj użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24f7c-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="24f7c-251">![Dodaj użytkownika](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="24f7c-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="24f7c-252">a.</span><span class="sxs-lookup"><span data-stu-id="24f7c-252">a.</span></span> <span data-ttu-id="24f7c-253">Typ **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup** i **działu** prawidłowy Azure konta AD, które chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="24f7c-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="24f7c-254">b.</span><span class="sxs-lookup"><span data-stu-id="24f7c-254">b.</span></span> <span data-ttu-id="24f7c-255">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="24f7c-256">Inne narzędzia do tworzenia ZScaler dwa konta użytkownika lub interfejsów API dostarczonych przez dwa ZScaler służy do obsługi administracyjnej kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24f7c-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="24f7c-257">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24f7c-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="24f7c-258">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do dwóch Zscaler.</span><span class="sxs-lookup"><span data-stu-id="24f7c-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Two.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="24f7c-260">**Aby przypisać Simona Britta do dwóch Zscaler, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24f7c-260">**To assign Britta Simon to Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="24f7c-261">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="24f7c-263">Na liście aplikacji zaznacz **Zscaler dwóch**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-263">In the applications list, select **Zscaler Two**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="24f7c-265">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="24f7c-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="24f7c-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24f7c-267">Click **Add** button.</span></span> <span data-ttu-id="24f7c-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="24f7c-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="24f7c-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="24f7c-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24f7c-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24f7c-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24f7c-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24f7c-273">Testing single sign-on</span></span>

<span data-ttu-id="24f7c-274">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="24f7c-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="24f7c-275">Po kliknięciu kafelka Zscaler dwóch w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Zscaler dwóch aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24f7c-275">When you click the Zscaler Two tile in the Access Panel, you should get automatically signed-on to your Zscaler Two application.</span></span>
<span data-ttu-id="24f7c-276">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24f7c-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24f7c-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="24f7c-277">Additional resources</span></span>

* [<span data-ttu-id="24f7c-278">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24f7c-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24f7c-279">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24f7c-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

