---
title: 'Samouczek: Integracji Azure Active Directory z Zscaler ZSCloud | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="ddddf-103">Samouczek: Integracji Azure Active Directory z Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="ddddf-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="ddddf-104">Z tego samouczka dowiesz się integrowanie Zscaler ZSCloud z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddddf-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddddf-105">Integracja z usługą Azure AD Zscaler ZSCloud zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ddddf-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ddddf-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="ddddf-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="ddddf-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Zscaler ZSCloud (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddddf-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddddf-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ddddf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ddddf-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddddf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddddf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ddddf-110">Prerequisites</span></span>

<span data-ttu-id="ddddf-111">Aby skonfigurować integrację usługi Azure AD z Zscaler ZSCloud, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ddddf-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="ddddf-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddddf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddddf-113">Zscaler ZSCloud logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ddddf-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddddf-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddddf-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ddddf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddddf-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ddddf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddddf-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddddf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddddf-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ddddf-118">Scenario description</span></span>
<span data-ttu-id="ddddf-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ddddf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddddf-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ddddf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddddf-121">Dodawanie Zscaler ZSCloud z galerii</span><span class="sxs-lookup"><span data-stu-id="ddddf-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="ddddf-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddddf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="ddddf-123">Dodawanie Zscaler ZSCloud z galerii</span><span class="sxs-lookup"><span data-stu-id="ddddf-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="ddddf-124">Aby skonfigurować integrację usługi Azure AD Zscaler ZSCloud, należy dodać Zscaler ZSCloud z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddddf-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ddddf-125">**Aby dodać Zscaler ZSCloud z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddddf-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ddddf-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddddf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ddddf-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ddddf-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ddddf-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ddddf-133">W polu wyszukiwania wpisz **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="ddddf-135">W panelu wyników wybierz **Zscaler ZSCloud**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ddddf-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddddf-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddddf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddddf-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ddddf-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddddf-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Zscaler ZSCloud jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddddf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="ddddf-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Zscaler ZSCloud musi się.</span><span class="sxs-lookup"><span data-stu-id="ddddf-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="ddddf-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="ddddf-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ddddf-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ddddf-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ddddf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ddddf-144">**[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings)**  — Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ddddf-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="ddddf-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ddddf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddddf-146">**[Tworzenie użytkownika testowego Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Zscaler ZSCloud, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddddf-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddddf-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ddddf-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddddf-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ddddf-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddddf-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddddf-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddddf-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="ddddf-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddddf-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ddddf-152">W portalu Azure na **Zscaler ZSCloud** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ddddf-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ddddf-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="ddddf-156">Na **Zscaler ZSCloud domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="ddddf-158">W **adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ddddf-159">Należy zaktualizować tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="ddddf-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ddddf-160">Skontaktuj się z [zespołem pomocy technicznej klienta ZSCloud Zscaler](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="ddddf-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="ddddf-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ddddf-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="ddddf-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddddf-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddddf-165">Na **Zscaler ZSCloud konfiguracji** kliknij **skonfigurować Zscaler ZSCloud** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ddddf-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ddddf-166">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ddddf-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="ddddf-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="ddddf-169">W menu u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="ddddf-170">![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="ddddf-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="ddddf-171">W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="ddddf-172">![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="ddddf-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="ddddf-173">W **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="ddddf-174">![Uwierzytelnianie](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="ddddf-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="ddddf-175">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-175">a.</span></span> <span data-ttu-id="ddddf-176">Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="ddddf-177">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-177">b.</span></span> <span data-ttu-id="ddddf-178">Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="ddddf-179">Na **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące czynności, a następnie kliknij **gotowe**</span><span class="sxs-lookup"><span data-stu-id="ddddf-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="ddddf-180">![Logowanie jednokrotne](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ddddf-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="ddddf-181">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-181">a.</span></span> <span data-ttu-id="ddddf-182">Wklej **SAML pojedynczy znak na adres URL usługi** wartości do **adres URL portalu SAML, do którego użytkownicy są wysyłane do uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="ddddf-183">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-183">b.</span></span> <span data-ttu-id="ddddf-184">W **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="ddddf-185">c.</span><span class="sxs-lookup"><span data-stu-id="ddddf-185">c.</span></span> <span data-ttu-id="ddddf-186">Aby przekazać certyfikat pobrany, kliknij przycisk **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="ddddf-187">d.</span><span class="sxs-lookup"><span data-stu-id="ddddf-187">d.</span></span> <span data-ttu-id="ddddf-188">Wybierz **Włącz SAML automatycznego inicjowania obsługi**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="ddddf-189">Na **skonfigurować uwierzytelnianie użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="ddddf-190">![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="ddddf-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="ddddf-191">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-191">a.</span></span> <span data-ttu-id="ddddf-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-192">Click **Save**.</span></span>

    <span data-ttu-id="ddddf-193">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-193">b.</span></span> <span data-ttu-id="ddddf-194">Kliknij przycisk **Aktywuj teraz**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="ddddf-195">Konfigurowanie ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="ddddf-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="ddddf-196">Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ddddf-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="ddddf-197">Uruchom **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="ddddf-198">Wybierz **Opcje internetowe** z **narzędzia** menu otwartego **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="ddddf-199">![Opcje internetowe](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opcje internetowe")</span><span class="sxs-lookup"><span data-stu-id="ddddf-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="ddddf-200">Kliknij przycisk **połączeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="ddddf-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="ddddf-201">![Połączenia](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "połączeń")</span><span class="sxs-lookup"><span data-stu-id="ddddf-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="ddddf-202">Kliknij przycisk **ustawienia sieci LAN** otworzyć **ustawienia sieci LAN** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="ddddf-203">W sekcji serwer Proxy wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="ddddf-204">![Serwer proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "serwera Proxy")</span><span class="sxs-lookup"><span data-stu-id="ddddf-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="ddddf-205">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-205">a.</span></span> <span data-ttu-id="ddddf-206">Wybierz **Użyj serwera proxy dla sieci LAN**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="ddddf-207">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-207">b.</span></span> <span data-ttu-id="ddddf-208">W polu tekstowym adres typu **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="ddddf-209">c.</span><span class="sxs-lookup"><span data-stu-id="ddddf-209">c.</span></span> <span data-ttu-id="ddddf-210">W polu tekstowym portu, wpisz **80**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="ddddf-211">d.</span><span class="sxs-lookup"><span data-stu-id="ddddf-211">d.</span></span> <span data-ttu-id="ddddf-212">Wybierz **używaj serwera proxy dla adresów lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="ddddf-213">e.</span><span class="sxs-lookup"><span data-stu-id="ddddf-213">e.</span></span> <span data-ttu-id="ddddf-214">Kliknij przycisk **OK** zamknąć **ustawienia sieci lokalnej (LAN)** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="ddddf-215">Kliknij przycisk **OK** zamknąć **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddddf-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddddf-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddddf-217">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ddddf-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ddddf-219">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddddf-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ddddf-220">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddddf-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddddf-222">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddddf-224">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddddf-226">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddddf-228">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-228">a.</span></span> <span data-ttu-id="ddddf-229">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddddf-230">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-230">b.</span></span> <span data-ttu-id="ddddf-231">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddddf-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddddf-232">c.</span><span class="sxs-lookup"><span data-stu-id="ddddf-232">c.</span></span> <span data-ttu-id="ddddf-233">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ddddf-234">d.</span><span class="sxs-lookup"><span data-stu-id="ddddf-234">d.</span></span> <span data-ttu-id="ddddf-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="ddddf-236">Tworzenie użytkownika testowego Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="ddddf-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="ddddf-237">Aby umożliwić użytkownikom usługi Azure AD zalogować się do ZScaler ZSCloud, muszą mieć przydzielone do ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="ddddf-238">W przypadku ZScaler ZSCloud Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ddddf-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="ddddf-239">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="ddddf-240">Zaloguj się do Twojego **Zscaler** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ddddf-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="ddddf-241">Kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="ddddf-242">![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="ddddf-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="ddddf-243">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="ddddf-244">![Dodaj](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="ddddf-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="ddddf-245">W **użytkowników** , kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="ddddf-246">![Dodaj](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="ddddf-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="ddddf-247">W sekcji Dodaj użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ddddf-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="ddddf-248">![Dodaj użytkownika](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="ddddf-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="ddddf-249">a.</span><span class="sxs-lookup"><span data-stu-id="ddddf-249">a.</span></span> <span data-ttu-id="ddddf-250">Typu **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup** i **działu** poprawnego konta usługi AAD chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="ddddf-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="ddddf-251">b.</span><span class="sxs-lookup"><span data-stu-id="ddddf-251">b.</span></span> <span data-ttu-id="ddddf-252">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ddddf-253">Możesz użyć innych ZScaler ZSCloud użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ZScaler ZSCloud do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ddddf-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ddddf-254">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddddf-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ddddf-255">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ddddf-257">**Aby przypisać Simona Britta Zscaler ZSCloud, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ddddf-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="ddddf-258">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ddddf-260">Na liście aplikacji zaznacz **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="ddddf-262">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ddddf-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ddddf-264">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddddf-264">Click **Add** button.</span></span> <span data-ttu-id="ddddf-265">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ddddf-267">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ddddf-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ddddf-268">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddddf-269">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddddf-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddddf-270">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddddf-270">Testing single sign-on</span></span>

<span data-ttu-id="ddddf-271">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="ddddf-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="ddddf-272">Po kliknięciu kafelka Zscaler ZSCloud w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="ddddf-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="ddddf-273">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ddddf-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ddddf-274">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ddddf-274">Additional resources</span></span>

* [<span data-ttu-id="ddddf-275">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddddf-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddddf-276">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddddf-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

