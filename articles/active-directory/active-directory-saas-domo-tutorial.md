---
title: 'Samouczek: Integracji Azure Active Directory z Domo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="1e5db-103">Samouczek: Integracji Azure Active Directory z Domo</span><span class="sxs-lookup"><span data-stu-id="1e5db-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="1e5db-104">Z tego samouczka dowiesz się integrowanie Domo z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e5db-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e5db-105">Integracja z usługą Azure AD Domo zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1e5db-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e5db-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Domo</span><span class="sxs-lookup"><span data-stu-id="1e5db-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="1e5db-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Domo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e5db-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e5db-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1e5db-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e5db-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e5db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e5db-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e5db-110">Prerequisites</span></span>

<span data-ttu-id="1e5db-111">Aby skonfigurować integrację usługi Azure AD z Domo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1e5db-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="1e5db-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e5db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e5db-113">Domo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1e5db-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e5db-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e5db-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1e5db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e5db-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1e5db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e5db-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e5db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e5db-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1e5db-118">Scenario description</span></span>
<span data-ttu-id="1e5db-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1e5db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e5db-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1e5db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e5db-121">Dodawanie Domo z galerii</span><span class="sxs-lookup"><span data-stu-id="1e5db-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="1e5db-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e5db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="1e5db-123">Dodawanie Domo z galerii</span><span class="sxs-lookup"><span data-stu-id="1e5db-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="1e5db-124">Aby skonfigurować integrację usługi Azure AD Domo, należy dodać Domo z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e5db-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e5db-125">**Aby dodać Domo z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e5db-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5db-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e5db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1e5db-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e5db-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1e5db-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1e5db-133">W polu wyszukiwania wpisz **Domo**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-133">In the search box, type **Domo**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="1e5db-135">W panelu wyników wybierz **Domo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1e5db-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e5db-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e5db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e5db-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Domo na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1e5db-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e5db-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Domo jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e5db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="1e5db-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Domo musi się.</span><span class="sxs-lookup"><span data-stu-id="1e5db-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="1e5db-141">W Domo, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1e5db-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e5db-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Domo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1e5db-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e5db-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e5db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e5db-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e5db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e5db-145">**[Tworzenie użytkownika testowego Domo](#creating-a-domo-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Domo połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e5db-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e5db-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1e5db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e5db-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1e5db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e5db-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e5db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e5db-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Domo.</span><span class="sxs-lookup"><span data-stu-id="1e5db-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="1e5db-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Domo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e5db-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5db-151">W portalu Azure na **Domo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1e5db-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1e5db-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="1e5db-155">Na **Domo domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e5db-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="1e5db-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e5db-157">a.</span></span> <span data-ttu-id="1e5db-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="1e5db-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="1e5db-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e5db-159">b.</span></span> <span data-ttu-id="1e5db-160">W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="1e5db-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="1e5db-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1e5db-161">These values are not real.</span></span> <span data-ttu-id="1e5db-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="1e5db-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e5db-163">Skontaktuj się z [zespołem pomocy technicznej klienta Domo](mailto:support@domo.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="1e5db-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="1e5db-164">Aplikacja Domo oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="1e5db-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1e5db-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e5db-165">Configure the following claims for this application.</span></span> <span data-ttu-id="1e5db-166">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e5db-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1e5db-167">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1e5db-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="1e5db-169">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e5db-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="1e5db-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="1e5db-170">Attribute Name</span></span> | <span data-ttu-id="1e5db-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="1e5db-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="1e5db-172">name</span><span class="sxs-lookup"><span data-stu-id="1e5db-172">name</span></span> | <span data-ttu-id="1e5db-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="1e5db-173">user.displayname</span></span> |
    | <span data-ttu-id="1e5db-174">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="1e5db-174">email</span></span> | <span data-ttu-id="1e5db-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="1e5db-175">user.mail</span></span> |
    
    <span data-ttu-id="1e5db-176">a.</span><span class="sxs-lookup"><span data-stu-id="1e5db-176">a.</span></span> <span data-ttu-id="1e5db-177">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1e5db-180">b.</span><span class="sxs-lookup"><span data-stu-id="1e5db-180">b.</span></span> <span data-ttu-id="1e5db-181">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="1e5db-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1e5db-182">c.</span><span class="sxs-lookup"><span data-stu-id="1e5db-182">c.</span></span> <span data-ttu-id="1e5db-183">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="1e5db-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1e5db-184">d.</span><span class="sxs-lookup"><span data-stu-id="1e5db-184">d.</span></span> <span data-ttu-id="1e5db-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="1e5db-186">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1e5db-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="1e5db-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e5db-188">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="1e5db-190">Na **konfiguracji Domo** , kliknij przycisk **skonfigurować Domo** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="1e5db-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1e5db-191">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="1e5db-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="1e5db-193">Skonfigurować logowanie jednokrotne w **Domo** stronie, musisz wysłać pobrany **certyfikatu**, **identyfikator jednostki SAML**, **SAML pojedynczy znak na adres URL usługi** i **Sign-Out adres URL** do [Domo zespołem pomocy technicznej](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="1e5db-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="1e5db-194">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="1e5db-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1e5db-195">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1e5db-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e5db-196">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1e5db-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e5db-197">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e5db-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e5db-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e5db-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e5db-199">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e5db-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1e5db-201">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e5db-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5db-202">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e5db-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e5db-204">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e5db-206">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e5db-208">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e5db-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e5db-210">a.</span><span class="sxs-lookup"><span data-stu-id="1e5db-210">a.</span></span> <span data-ttu-id="1e5db-211">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e5db-212">b.</span><span class="sxs-lookup"><span data-stu-id="1e5db-212">b.</span></span> <span data-ttu-id="1e5db-213">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e5db-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e5db-214">c.</span><span class="sxs-lookup"><span data-stu-id="1e5db-214">c.</span></span> <span data-ttu-id="1e5db-215">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e5db-216">d.</span><span class="sxs-lookup"><span data-stu-id="1e5db-216">d.</span></span> <span data-ttu-id="1e5db-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="1e5db-218">Tworzenie użytkownika testowego Domo</span><span class="sxs-lookup"><span data-stu-id="1e5db-218">Creating a Domo test user</span></span>

<span data-ttu-id="1e5db-219">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Domo.</span><span class="sxs-lookup"><span data-stu-id="1e5db-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="1e5db-220">Domo obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="1e5db-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1e5db-221">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e5db-221">There is no action item for you in this section.</span></span> <span data-ttu-id="1e5db-222">Nowy użytkownik został utworzony podczas próby dostępu Domo, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1e5db-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e5db-223">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e5db-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e5db-224">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Domo.</span><span class="sxs-lookup"><span data-stu-id="1e5db-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1e5db-226">**Aby przypisać Simona Britta Domo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e5db-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5db-227">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1e5db-229">Na liście aplikacji zaznacz **Domo**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-229">In the applications list, select **Domo**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="1e5db-231">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1e5db-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1e5db-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e5db-233">Click **Add** button.</span></span> <span data-ttu-id="1e5db-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1e5db-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1e5db-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e5db-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e5db-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e5db-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e5db-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e5db-239">Testing single sign-on</span></span>

<span data-ttu-id="1e5db-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1e5db-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="1e5db-241">Po kliknięciu kafelka Domo w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Domo.</span><span class="sxs-lookup"><span data-stu-id="1e5db-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="1e5db-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e5db-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1e5db-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1e5db-243">Additional resources</span></span>

* [<span data-ttu-id="1e5db-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e5db-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e5db-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e5db-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

