---
title: 'Samouczek: Integracji Azure Active Directory z Onit | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="83652-103">Samouczek: Integracji Azure Active Directory z Onit</span><span class="sxs-lookup"><span data-stu-id="83652-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="83652-104">Z tego samouczka dowiesz się integrowanie Onit z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83652-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83652-105">Integracja z usługą Azure AD Onit zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="83652-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83652-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Onit.</span><span class="sxs-lookup"><span data-stu-id="83652-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="83652-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Onit (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83652-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="83652-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83652-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="83652-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83652-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83652-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83652-110">Prerequisites</span></span>

<span data-ttu-id="83652-111">Aby skonfigurować integrację usługi Azure AD z Onit, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="83652-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="83652-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83652-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83652-113">Onit logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="83652-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83652-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="83652-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83652-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="83652-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83652-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="83652-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83652-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83652-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83652-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="83652-118">Scenario description</span></span>

<span data-ttu-id="83652-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="83652-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83652-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="83652-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83652-121">Dodawanie Onit z galerii</span><span class="sxs-lookup"><span data-stu-id="83652-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="83652-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="83652-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="83652-123">Dodawanie Onit z galerii</span><span class="sxs-lookup"><span data-stu-id="83652-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="83652-124">Aby skonfigurować integrację usługi Azure AD Onit, należy dodać Onit z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="83652-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83652-125">**Aby dodać Onit z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="83652-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83652-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="83652-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="83652-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="83652-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83652-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="83652-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="83652-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83652-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="83652-133">W polu wyszukiwania wpisz **Onit**, wybierz pozycję **Onit** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="83652-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![Onit na liście wyników](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="83652-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="83652-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="83652-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Onit na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="83652-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83652-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Onit jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83652-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="83652-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Onit musi się.</span><span class="sxs-lookup"><span data-stu-id="83652-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="83652-139">W Onit, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="83652-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83652-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Onit, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="83652-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83652-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="83652-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83652-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="83652-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83652-143">**[Tworzenie użytkownika testowego Onit](#create-an-onit-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Onit połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="83652-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83652-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="83652-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83652-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="83652-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="83652-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="83652-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="83652-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Onit.</span><span class="sxs-lookup"><span data-stu-id="83652-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="83652-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Onit, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="83652-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="83652-149">W portalu Azure na **Onit** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="83652-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="83652-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="83652-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="83652-153">Na **Onit domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83652-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny onit pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="83652-155">a.</span><span class="sxs-lookup"><span data-stu-id="83652-155">a.</span></span> <span data-ttu-id="83652-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="83652-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="83652-157">b.</span><span class="sxs-lookup"><span data-stu-id="83652-157">b.</span></span> <span data-ttu-id="83652-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="83652-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83652-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="83652-159">These values are not real.</span></span> <span data-ttu-id="83652-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="83652-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83652-161">Skontaktuj się z [zespołem pomocy technicznej klienta Onit](https://www.onit.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="83652-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="83652-162">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="83652-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="83652-164">Aplikacja onit oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="83652-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="83652-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83652-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="83652-166">Możesz zarządzać wartości tych atrybutów z **"Atrribute"** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83652-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="83652-167">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="83652-167">The following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="83652-169">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83652-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="83652-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="83652-170">Attribute Name</span></span> | <span data-ttu-id="83652-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="83652-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="83652-172">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="83652-172">email</span></span> | <span data-ttu-id="83652-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="83652-173">user.mail</span></span> |
    
    <span data-ttu-id="83652-174">a.</span><span class="sxs-lookup"><span data-stu-id="83652-174">a.</span></span> <span data-ttu-id="83652-175">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83652-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="83652-178">b.</span><span class="sxs-lookup"><span data-stu-id="83652-178">b.</span></span> <span data-ttu-id="83652-179">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="83652-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="83652-180">c.</span><span class="sxs-lookup"><span data-stu-id="83652-180">c.</span></span> <span data-ttu-id="83652-181">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="83652-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="83652-182">d.</span><span class="sxs-lookup"><span data-stu-id="83652-182">d.</span></span> <span data-ttu-id="83652-183">Pozostaw **Namespace** puste.</span><span class="sxs-lookup"><span data-stu-id="83652-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="83652-184">e.</span><span class="sxs-lookup"><span data-stu-id="83652-184">e.</span></span> <span data-ttu-id="83652-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="83652-185">Click **Ok**.</span></span>

7. <span data-ttu-id="83652-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="83652-186">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="83652-188">Na **konfiguracji Onit** , kliknij przycisk **skonfigurować Onit** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="83652-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="83652-189">Kopiuj **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="83652-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="83652-191">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Onit jako administrator.</span><span class="sxs-lookup"><span data-stu-id="83652-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="83652-192">W menu u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="83652-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="83652-193">![Administracja](./media/active-directory-saas-onit-tutorial/IC791174.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="83652-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="83652-194">Kliknij przycisk **Corporation edycji**.</span><span class="sxs-lookup"><span data-stu-id="83652-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="83652-195">![Edytuj Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Corporation edycji")</span><span class="sxs-lookup"><span data-stu-id="83652-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="83652-196">Kliknij przycisk **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="83652-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="83652-197">![Informacje o firmie edycji](./media/active-directory-saas-onit-tutorial/IC791176.png "informacji o firmie edycji")</span><span class="sxs-lookup"><span data-stu-id="83652-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="83652-198">Na **zabezpieczeń** karcie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83652-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="83652-199">![Logowanie jednokrotne](./media/active-directory-saas-onit-tutorial/IC791177.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="83652-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="83652-200">a.</span><span class="sxs-lookup"><span data-stu-id="83652-200">a.</span></span> <span data-ttu-id="83652-201">Jako **strategii uwierzytelniania**, wybierz pozycję **rejestracji jednokrotnej i hasło**.</span><span class="sxs-lookup"><span data-stu-id="83652-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="83652-202">b.</span><span class="sxs-lookup"><span data-stu-id="83652-202">b.</span></span> <span data-ttu-id="83652-203">W **Idp docelowy adres URL** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83652-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="83652-204">c.</span><span class="sxs-lookup"><span data-stu-id="83652-204">c.</span></span> <span data-ttu-id="83652-205">W **adresu URL wylogowania Idp** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83652-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="83652-206">d.</span><span class="sxs-lookup"><span data-stu-id="83652-206">d.</span></span> <span data-ttu-id="83652-207">W **odcisk palca certyfikatu Idp (SHA1)** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83652-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="83652-208">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="83652-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83652-209">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="83652-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83652-210">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83652-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="83652-211">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83652-211">Create an Azure AD test user</span></span>

<span data-ttu-id="83652-212">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="83652-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="83652-214">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="83652-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83652-215">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="83652-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="83652-217">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="83652-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="83652-219">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="83652-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="83652-221">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83652-221">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="83652-223">a.</span><span class="sxs-lookup"><span data-stu-id="83652-223">a.</span></span> <span data-ttu-id="83652-224">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83652-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83652-225">b.</span><span class="sxs-lookup"><span data-stu-id="83652-225">b.</span></span> <span data-ttu-id="83652-226">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="83652-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="83652-227">c.</span><span class="sxs-lookup"><span data-stu-id="83652-227">c.</span></span> <span data-ttu-id="83652-228">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="83652-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="83652-229">d.</span><span class="sxs-lookup"><span data-stu-id="83652-229">d.</span></span> <span data-ttu-id="83652-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83652-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="83652-231">Tworzenie użytkownika testowego Onit</span><span class="sxs-lookup"><span data-stu-id="83652-231">Create an Onit test user</span></span>

<span data-ttu-id="83652-232">Aby włączyć użytkowników usługi Azure AD zalogować się do Onit, musi być przygotowana do Onit.</span><span class="sxs-lookup"><span data-stu-id="83652-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="83652-233">W przypadku Onit Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="83652-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="83652-234">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="83652-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="83652-235">Zaloguj się na Twojej **Onit** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="83652-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="83652-236">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="83652-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="83652-237">![Administracja](./media/active-directory-saas-onit-tutorial/IC791180.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="83652-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="83652-238">Na **Dodaj użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="83652-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="83652-239">![Dodaj użytkownika](./media/active-directory-saas-onit-tutorial/IC791181.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="83652-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="83652-240">Typ **nazwa** i **adres E-mail** prawidłowy Azure konta AD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="83652-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="83652-241">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83652-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="83652-242">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="83652-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="83652-243">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83652-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="83652-244">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Onit.</span><span class="sxs-lookup"><span data-stu-id="83652-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="83652-246">**Aby przypisać Simona Britta Onit, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="83652-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="83652-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="83652-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="83652-249">Na liście aplikacji zaznacz **Onit**.</span><span class="sxs-lookup"><span data-stu-id="83652-249">In the applications list, select **Onit**.</span></span>

    ![Łącze Onit na liście aplikacji](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="83652-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="83652-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="83652-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="83652-253">Click **Add** button.</span></span> <span data-ttu-id="83652-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83652-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="83652-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="83652-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83652-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83652-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83652-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83652-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="83652-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="83652-259">Test single sign-on</span></span>

<span data-ttu-id="83652-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="83652-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="83652-261">Po kliknięciu kafelka Onit w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Onit.</span><span class="sxs-lookup"><span data-stu-id="83652-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="83652-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83652-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83652-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="83652-263">Additional resources</span></span>

* [<span data-ttu-id="83652-264">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83652-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83652-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83652-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

