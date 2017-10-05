---
title: 'Samouczek: Integracji Azure Active Directory z Veracode | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="bfa53-103">Samouczek: Integracji Azure Active Directory z Veracode</span><span class="sxs-lookup"><span data-stu-id="bfa53-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="bfa53-104">Z tego samouczka dowiesz się integrowanie Veracode z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfa53-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfa53-105">Integracja z usługą Azure AD Veracode zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bfa53-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bfa53-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Veracode.</span><span class="sxs-lookup"><span data-stu-id="bfa53-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="bfa53-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Veracode (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfa53-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bfa53-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa53-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bfa53-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfa53-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfa53-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bfa53-110">Prerequisites</span></span>

<span data-ttu-id="bfa53-111">Aby skonfigurować integrację usługi Azure AD z Veracode, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bfa53-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="bfa53-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfa53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfa53-113">Veracode logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bfa53-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfa53-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfa53-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bfa53-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfa53-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bfa53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfa53-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfa53-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfa53-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bfa53-118">Scenario description</span></span>
<span data-ttu-id="bfa53-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bfa53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfa53-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bfa53-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfa53-121">Dodaj Veracode z galerii</span><span class="sxs-lookup"><span data-stu-id="bfa53-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="bfa53-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfa53-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="bfa53-123">Dodaj Veracode z galerii</span><span class="sxs-lookup"><span data-stu-id="bfa53-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="bfa53-124">Aby skonfigurować integrację usługi Azure AD Veracode, należy dodać Veracode z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfa53-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bfa53-125">**Aby dodać Veracode z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfa53-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bfa53-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bfa53-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="bfa53-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bfa53-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="bfa53-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="bfa53-133">W polu wyszukiwania wpisz **Veracode**, wybierz pozycję **Veracode** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bfa53-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode na liście wyników](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bfa53-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfa53-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bfa53-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Veracode w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bfa53-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Veracode jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfa53-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="bfa53-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Veracode musi się.</span><span class="sxs-lookup"><span data-stu-id="bfa53-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="bfa53-139">W Veracode, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bfa53-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bfa53-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Veracode, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bfa53-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bfa53-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bfa53-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bfa53-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfa53-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfa53-143">**[Tworzenie użytkownika testowego Veracode](#create-a-veracode-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Veracode połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfa53-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfa53-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bfa53-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfa53-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bfa53-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bfa53-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfa53-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bfa53-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Veracode.</span><span class="sxs-lookup"><span data-stu-id="bfa53-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="bfa53-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Veracode, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfa53-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="bfa53-149">W portalu Azure na **Veracode** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="bfa53-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bfa53-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="bfa53-153">Na **Veracode domeny i adres URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa53-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="bfa53-155">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bfa53-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="bfa53-157">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Veracode do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="bfa53-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="bfa53-158">Aplikacja Veracode oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu saml** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bfa53-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="bfa53-159">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="bfa53-160">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="bfa53-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="bfa53-161">Aby dodać mapowania wymaganego atrybutu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa53-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="bfa53-162">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="bfa53-162">Attribute Name</span></span> | <span data-ttu-id="bfa53-163">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="bfa53-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="bfa53-164">Imię</span><span class="sxs-lookup"><span data-stu-id="bfa53-164">firstname</span></span> |<span data-ttu-id="bfa53-165">User.givenName</span><span class="sxs-lookup"><span data-stu-id="bfa53-165">User.givenname</span></span> |
    | <span data-ttu-id="bfa53-166">nazwisko</span><span class="sxs-lookup"><span data-stu-id="bfa53-166">lastname</span></span> |<span data-ttu-id="bfa53-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="bfa53-167">User.surname</span></span> |
    | <span data-ttu-id="bfa53-168">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="bfa53-168">email</span></span> |<span data-ttu-id="bfa53-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="bfa53-169">User.mail</span></span> |
    
    <span data-ttu-id="bfa53-170">a.</span><span class="sxs-lookup"><span data-stu-id="bfa53-170">a.</span></span> <span data-ttu-id="bfa53-171">Dla każdego wiersza danych w tabeli powyżej, kliknij przycisk **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="bfa53-172">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="bfa53-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="bfa53-173">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="bfa53-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="bfa53-174">b.</span><span class="sxs-lookup"><span data-stu-id="bfa53-174">b.</span></span> <span data-ttu-id="bfa53-175">W **nazwa atrybutu** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bfa53-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bfa53-176">c.</span><span class="sxs-lookup"><span data-stu-id="bfa53-176">c.</span></span> <span data-ttu-id="bfa53-177">W **wartość atrybutu** pole tekstowe, wybierz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bfa53-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bfa53-178">d.</span><span class="sxs-lookup"><span data-stu-id="bfa53-178">d.</span></span> <span data-ttu-id="bfa53-179">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-179">Click **Ok**.</span></span>

7. <span data-ttu-id="bfa53-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfa53-180">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bfa53-182">Na **konfiguracji Veracode** , kliknij przycisk **skonfigurować Veracode** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bfa53-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bfa53-183">Kopiuj **identyfikator jednostki SAML** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bfa53-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="bfa53-185">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Veracode jako administrator.</span><span class="sxs-lookup"><span data-stu-id="bfa53-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="bfa53-186">W menu u góry kliknij **ustawienia**, a następnie kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="bfa53-187">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802911.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="bfa53-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="bfa53-188">Kliknij przycisk **SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="bfa53-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="bfa53-189">W **ustawienia SAML organizacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa53-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="bfa53-190">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802912.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="bfa53-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="bfa53-191">a.</span><span class="sxs-lookup"><span data-stu-id="bfa53-191">a.</span></span>  <span data-ttu-id="bfa53-192">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa53-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="bfa53-193">b.</span><span class="sxs-lookup"><span data-stu-id="bfa53-193">b.</span></span> <span data-ttu-id="bfa53-194">Aby przekazać certyfikat pobrany z portalu Azure, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="bfa53-195">c.</span><span class="sxs-lookup"><span data-stu-id="bfa53-195">c.</span></span> <span data-ttu-id="bfa53-196">Wybierz **umożliwić samodzielną rejestrację**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="bfa53-197">W **ustawień rejestracji samoobsługowego** sekcji, wykonaj następujące czynności, a następnie kliknij przycisk **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="bfa53-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="bfa53-198">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802913.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="bfa53-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="bfa53-199">a.</span><span class="sxs-lookup"><span data-stu-id="bfa53-199">a.</span></span> <span data-ttu-id="bfa53-200">Jako **nowe Aktywacja użytkownika**, wybierz pozycję **wymagane uaktywnienie nr**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="bfa53-201">b.</span><span class="sxs-lookup"><span data-stu-id="bfa53-201">b.</span></span> <span data-ttu-id="bfa53-202">Jako **aktualizacje danych użytkownika**, wybierz pozycję **dane użytkownika Veracode preferencji**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="bfa53-203">c.</span><span class="sxs-lookup"><span data-stu-id="bfa53-203">c.</span></span> <span data-ttu-id="bfa53-204">Aby uzyskać **szczegółów atrybutów SAML**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa53-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="bfa53-205">**Role użytkowników**</span><span class="sxs-lookup"><span data-stu-id="bfa53-205">**User Roles**</span></span>
      * <span data-ttu-id="bfa53-206">**Administrator zasad**</span><span class="sxs-lookup"><span data-stu-id="bfa53-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="bfa53-207">**Osoba dokonująca przeglądu**</span><span class="sxs-lookup"><span data-stu-id="bfa53-207">**Reviewer**</span></span>
      * <span data-ttu-id="bfa53-208">**Realizacji zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="bfa53-208">**Security Lead**</span></span>
      * <span data-ttu-id="bfa53-209">**Główna programu SMS**</span><span class="sxs-lookup"><span data-stu-id="bfa53-209">**Executive**</span></span>
      * <span data-ttu-id="bfa53-210">**Obiekt przesyłający**</span><span class="sxs-lookup"><span data-stu-id="bfa53-210">**Submitter**</span></span>
      * <span data-ttu-id="bfa53-211">**Twórcy**</span><span class="sxs-lookup"><span data-stu-id="bfa53-211">**Creator**</span></span>
      * <span data-ttu-id="bfa53-212">**Wszystkie typy skanowania**</span><span class="sxs-lookup"><span data-stu-id="bfa53-212">**All Scan Types**</span></span>
      * <span data-ttu-id="bfa53-213">**Członkostwo zespołu**</span><span class="sxs-lookup"><span data-stu-id="bfa53-213">**Team Memberships**</span></span>
      * <span data-ttu-id="bfa53-214">**Domyślny zespół**</span><span class="sxs-lookup"><span data-stu-id="bfa53-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="bfa53-215">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bfa53-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bfa53-216">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bfa53-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bfa53-217">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfa53-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bfa53-218">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfa53-218">Create an Azure AD test user</span></span>

<span data-ttu-id="bfa53-219">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfa53-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="bfa53-221">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfa53-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bfa53-222">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfa53-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bfa53-224">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bfa53-226">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bfa53-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bfa53-228">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bfa53-228">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bfa53-230">a.</span><span class="sxs-lookup"><span data-stu-id="bfa53-230">a.</span></span> <span data-ttu-id="bfa53-231">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfa53-232">b.</span><span class="sxs-lookup"><span data-stu-id="bfa53-232">b.</span></span> <span data-ttu-id="bfa53-233">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bfa53-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bfa53-234">c.</span><span class="sxs-lookup"><span data-stu-id="bfa53-234">c.</span></span> <span data-ttu-id="bfa53-235">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="bfa53-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bfa53-236">d.</span><span class="sxs-lookup"><span data-stu-id="bfa53-236">d.</span></span> <span data-ttu-id="bfa53-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="bfa53-238">Tworzenie użytkownika testowego Veracode</span><span class="sxs-lookup"><span data-stu-id="bfa53-238">Create a Veracode test user</span></span>
<span data-ttu-id="bfa53-239">Aby włączyć użytkowników usługi Azure AD zalogować się do Veracode, musi być przygotowana do Veracode.</span><span class="sxs-lookup"><span data-stu-id="bfa53-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="bfa53-240">W przypadku Veracode Inicjowanie obsługi to zadanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="bfa53-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="bfa53-241">Nie ma elementu akcji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="bfa53-241">There is no action item for you.</span></span> <span data-ttu-id="bfa53-242">Użytkownicy są tworzone automatycznie w razie potrzeby podczas pierwszej pojedynczego logowania jednokrotnego próby.</span><span class="sxs-lookup"><span data-stu-id="bfa53-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa53-243">Możesz użyć innych Veracode użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Veracode do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfa53-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bfa53-244">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfa53-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="bfa53-245">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Veracode.</span><span class="sxs-lookup"><span data-stu-id="bfa53-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="bfa53-247">**Aby przypisać Simona Britta Veracode, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bfa53-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="bfa53-248">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bfa53-250">Na liście aplikacji zaznacz **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-250">In the applications list, select **Veracode**.</span></span>

    ![Łącze Veracode na liście aplikacji](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="bfa53-252">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bfa53-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="bfa53-254">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfa53-254">Click **Add** button.</span></span> <span data-ttu-id="bfa53-255">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="bfa53-257">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bfa53-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bfa53-258">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfa53-259">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bfa53-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bfa53-260">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bfa53-260">Test single sign-on</span></span>

<span data-ttu-id="bfa53-261">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bfa53-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bfa53-262">Po kliknięciu kafelka Veracode w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Veracode.</span><span class="sxs-lookup"><span data-stu-id="bfa53-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="bfa53-263">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfa53-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bfa53-264">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bfa53-264">Additional resources</span></span>

* [<span data-ttu-id="bfa53-265">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfa53-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfa53-266">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfa53-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

