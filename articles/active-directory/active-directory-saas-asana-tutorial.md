---
title: 'Samouczek: Integracji Azure Active Directory z Asana | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: a2f0cecb93cc382bcfd710c44eb70f80ae67f9b6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="5bebd-103">Samouczek: Integracji Azure Active Directory z Asana</span><span class="sxs-lookup"><span data-stu-id="5bebd-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="5bebd-104">Z tego samouczka dowiesz się integrowanie Asana z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bebd-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bebd-105">Integracja z usługą Azure AD Asana zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bebd-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bebd-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Asana</span><span class="sxs-lookup"><span data-stu-id="5bebd-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="5bebd-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Asana (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bebd-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bebd-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bebd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bebd-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bebd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bebd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bebd-110">Prerequisites</span></span>

<span data-ttu-id="5bebd-111">Aby skonfigurować integrację usługi Azure AD z Asana, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bebd-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="5bebd-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bebd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bebd-113">Asana jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bebd-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bebd-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bebd-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bebd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bebd-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bebd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bebd-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bebd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bebd-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bebd-118">Scenario description</span></span>
<span data-ttu-id="5bebd-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bebd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bebd-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bebd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bebd-121">Dodawanie Asana z galerii</span><span class="sxs-lookup"><span data-stu-id="5bebd-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="5bebd-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bebd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="5bebd-123">Dodawanie Asana z galerii</span><span class="sxs-lookup"><span data-stu-id="5bebd-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="5bebd-124">Aby skonfigurować integrację usługi Azure AD Asana, należy dodać Asana z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bebd-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bebd-125">**Aby dodać Asana z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bebd-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bebd-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bebd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="5bebd-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bebd-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="5bebd-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="5bebd-133">W polu wyszukiwania wpisz **Asana**, wybierz pozycję **Asana** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5bebd-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5bebd-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bebd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5bebd-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Asana na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5bebd-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bebd-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Asana jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bebd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="5bebd-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Asana musi się.</span><span class="sxs-lookup"><span data-stu-id="5bebd-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="5bebd-139">W Asana, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5bebd-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5bebd-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Asana, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5bebd-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bebd-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bebd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bebd-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bebd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bebd-143">**[Tworzenie użytkownika testowego Asana](#create-an-asana-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Asana połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bebd-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bebd-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bebd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bebd-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5bebd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5bebd-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bebd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5bebd-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="5bebd-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Asana, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bebd-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="5bebd-149">W portalu Azure na **Asana** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bebd-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5bebd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="5bebd-153">Na **Asana domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bebd-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Asana pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="5bebd-155">a.</span><span class="sxs-lookup"><span data-stu-id="5bebd-155">a.</span></span> <span data-ttu-id="5bebd-156">W **adres URL logowania** pole tekstowe, wprowadź adres URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="5bebd-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="5bebd-157">b.</span><span class="sxs-lookup"><span data-stu-id="5bebd-157">b.</span></span> <span data-ttu-id="5bebd-158">W **identyfikator** pole tekstowe, wartość typu:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="5bebd-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="5bebd-159">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bebd-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="5bebd-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bebd-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bebd-163">Na **konfiguracji Asana** , kliknij przycisk **skonfigurować Asana** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5bebd-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5bebd-164">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5bebd-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="5bebd-166">W oknie innej przeglądarki logowanie do aplikacji Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="5bebd-167">Aby skonfigurować logowanie Jednokrotne w Asana, uzyskać dostęp do ustawień obszaru roboczego, klikając nazwę obszaru roboczego w prawym górnym rogu ekranu.</span><span class="sxs-lookup"><span data-stu-id="5bebd-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="5bebd-168">Następnie kliknij  **\<nazwa obszaru roboczego\> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Ustawienia logowania jednokrotnego Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="5bebd-170">Na **ustawienia organizacji** okna, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="5bebd-171">Następnie kliknij przycisk **elementów członkowskich należy zalogować się za pośrednictwem SAML** umożliwiające konfigurację logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="5bebd-172">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bebd-172">The perform the following steps:</span></span>
   
    ![Skonfiguruj ustawienia organizacji rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="5bebd-174">a.</span><span class="sxs-lookup"><span data-stu-id="5bebd-174">a.</span></span> <span data-ttu-id="5bebd-175">W **adres URL logowania strony** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="5bebd-176">b.</span><span class="sxs-lookup"><span data-stu-id="5bebd-176">b.</span></span> <span data-ttu-id="5bebd-177">Kliknij prawym przyciskiem myszy certyfikat pobrany z portalu Azure, a następnie otwórz plik certyfikatu w Notatniku lub w edytorze tekstów preferowany.</span><span class="sxs-lookup"><span data-stu-id="5bebd-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="5bebd-178">Kopiowanie zawartości między rozpoczęcia i zakończenia tytuł certyfikatu, a następnie wklej je **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="5bebd-179">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-179">Click **Save**.</span></span> <span data-ttu-id="5bebd-180">Przejdź do [Asana przewodnik konfigurowania rejestracji Jednokrotnej](https://asana.com/guide/help/premium/authentication#gl-saml) Jeœli potrzebujesz dodatkowej pomocy.</span><span class="sxs-lookup"><span data-stu-id="5bebd-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="5bebd-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5bebd-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bebd-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5bebd-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bebd-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bebd-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5bebd-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bebd-184">Create an Azure AD test user</span></span>

<span data-ttu-id="5bebd-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bebd-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="5bebd-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bebd-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bebd-188">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bebd-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bebd-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bebd-192">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bebd-194">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bebd-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bebd-196">a.</span><span class="sxs-lookup"><span data-stu-id="5bebd-196">a.</span></span> <span data-ttu-id="5bebd-197">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bebd-198">b.</span><span class="sxs-lookup"><span data-stu-id="5bebd-198">b.</span></span> <span data-ttu-id="5bebd-199">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bebd-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bebd-200">c.</span><span class="sxs-lookup"><span data-stu-id="5bebd-200">c.</span></span> <span data-ttu-id="5bebd-201">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bebd-202">d.</span><span class="sxs-lookup"><span data-stu-id="5bebd-202">d.</span></span> <span data-ttu-id="5bebd-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="5bebd-204">Tworzenie użytkownika testowego Asana</span><span class="sxs-lookup"><span data-stu-id="5bebd-204">Create an Asana test user</span></span>

<span data-ttu-id="5bebd-205">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="5bebd-206">Na **Asana**, przejdź do **zespołów** sekcji w lewym panelu.</span><span class="sxs-lookup"><span data-stu-id="5bebd-206">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="5bebd-207">Kliknij przycisk ze znakiem plus.</span><span class="sxs-lookup"><span data-stu-id="5bebd-207">Click the plus sign button.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="5bebd-209">Wpisz adres e-mail britta.simon@contoso.com w polu tekstowym, a następnie wybierz **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-209">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

3. <span data-ttu-id="5bebd-210">Kliknij przycisk **wysłać zaproszenie**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-210">Click **Send Invite**.</span></span> <span data-ttu-id="5bebd-211">Nowy użytkownik otrzyma wiadomość e-mail na swoje konto e-mail.</span><span class="sxs-lookup"><span data-stu-id="5bebd-211">The new user will receive an email into her email account.</span></span> <span data-ttu-id="5bebd-212">Użytkownik należy utworzyć i zweryfikować konto.</span><span class="sxs-lookup"><span data-stu-id="5bebd-212">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5bebd-213">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bebd-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="5bebd-214">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![Przypisanie roli użytkownika][200]

<span data-ttu-id="5bebd-216">**Aby przypisać Simona Britta Asana, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bebd-216">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="5bebd-217">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bebd-219">Na liście aplikacji zaznacz **Asana**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-219">In the applications list, select **Asana**.</span></span>

    ![Łącze Asana na liście aplikacji](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="5bebd-221">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="5bebd-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bebd-223">Click **Add** button.</span></span> <span data-ttu-id="5bebd-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="5bebd-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5bebd-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bebd-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bebd-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bebd-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5bebd-229">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bebd-229">Test single sign-on</span></span>

<span data-ttu-id="5bebd-230">Celem tej sekcji służy do testowania programu Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bebd-230">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="5bebd-231">Przejdź do strony logowania Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-231">Go to Asana login page.</span></span> <span data-ttu-id="5bebd-232">W polu tekstowym Adres E-mail, Wstaw adres e-mail britta.simon@contoso.com. Pozostaw pole tekstowe hasła w puste, a następnie kliknij przycisk **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="5bebd-232">In the Email address textbox, insert the email address britta.simon@contoso.com. Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="5bebd-233">Nastąpi przekierowanie do strony logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bebd-233">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="5bebd-234">Ukończ poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bebd-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="5bebd-235">Teraz użytkownik jest zalogowany na Asana.</span><span class="sxs-lookup"><span data-stu-id="5bebd-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bebd-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bebd-236">Additional resources</span></span>

* [<span data-ttu-id="5bebd-237">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bebd-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bebd-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bebd-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
