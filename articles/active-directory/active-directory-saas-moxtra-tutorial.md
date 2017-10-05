---
title: 'Samouczek: Integracji Azure Active Directory z Moxtra | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="6846b-103">Samouczek: Integracji Azure Active Directory z Moxtra</span><span class="sxs-lookup"><span data-stu-id="6846b-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="6846b-104">Z tego samouczka dowiesz się integrowanie Moxtra z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6846b-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6846b-105">Integracja z usługą Azure AD Moxtra zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6846b-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6846b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Moxtra</span><span class="sxs-lookup"><span data-stu-id="6846b-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="6846b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Moxtra (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6846b-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6846b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6846b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6846b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6846b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6846b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6846b-110">Prerequisites</span></span>

<span data-ttu-id="6846b-111">Aby skonfigurować integrację usługi Azure AD z Moxtra, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6846b-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="6846b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6846b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6846b-113">Moxtra logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6846b-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6846b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6846b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6846b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6846b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6846b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6846b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6846b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6846b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6846b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6846b-118">Scenario description</span></span>
<span data-ttu-id="6846b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6846b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6846b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6846b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6846b-121">Dodawanie Moxtra z galerii</span><span class="sxs-lookup"><span data-stu-id="6846b-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="6846b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6846b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="6846b-123">Dodawanie Moxtra z galerii</span><span class="sxs-lookup"><span data-stu-id="6846b-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="6846b-124">Aby skonfigurować integrację usługi Azure AD Moxtra, należy dodać Moxtra z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6846b-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6846b-125">**Aby dodać Moxtra z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6846b-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6846b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6846b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6846b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6846b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6846b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6846b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6846b-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6846b-133">W polu wyszukiwania wpisz **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="6846b-133">In the search box, type **Moxtra**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="6846b-135">W panelu wyników wybierz **Moxtra**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6846b-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6846b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6846b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6846b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Moxtra w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6846b-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Moxtra jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6846b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="6846b-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Moxtra musi się.</span><span class="sxs-lookup"><span data-stu-id="6846b-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="6846b-141">W Moxtra, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="6846b-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6846b-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Moxtra, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6846b-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6846b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6846b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6846b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6846b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6846b-145">**[Tworzenie użytkownika testowego Moxtra](#creating-a-moxtra-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Moxtra połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6846b-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6846b-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6846b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6846b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6846b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6846b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6846b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6846b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Moxtra.</span><span class="sxs-lookup"><span data-stu-id="6846b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="6846b-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Moxtra, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6846b-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6846b-151">W portalu Azure na **Moxtra** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6846b-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6846b-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6846b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="6846b-155">Na **Moxtra domeny i adres URL** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6846b-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="6846b-157">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="6846b-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="6846b-158">Aplikacja Moxtra oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="6846b-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="6846b-159">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6846b-159">Configure the following claims for this application.</span></span> <span data-ttu-id="6846b-160">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6846b-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6846b-161">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6846b-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="6846b-163">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6846b-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="6846b-164">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="6846b-164">Attribute Name</span></span> | <span data-ttu-id="6846b-165">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="6846b-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6846b-166">Imię</span><span class="sxs-lookup"><span data-stu-id="6846b-166">firstname</span></span> | <span data-ttu-id="6846b-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="6846b-167">user.givenname</span></span> |
    | <span data-ttu-id="6846b-168">nazwisko</span><span class="sxs-lookup"><span data-stu-id="6846b-168">lastname</span></span> | <span data-ttu-id="6846b-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="6846b-169">user.surname</span></span> |
    | <span data-ttu-id="6846b-170">idpid</span><span class="sxs-lookup"><span data-stu-id="6846b-170">idpid</span></span>    | <span data-ttu-id="6846b-171">< Identyfikator jednostki SAML ></span><span class="sxs-lookup"><span data-stu-id="6846b-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="6846b-172">Wartość **idpid** atrybut nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6846b-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="6846b-173">Można uzyskać wartość rzeczywista z **krótkimi opisami** w obszarze **Moxtra konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="6846b-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="6846b-174">a.</span><span class="sxs-lookup"><span data-stu-id="6846b-174">a.</span></span> <span data-ttu-id="6846b-175">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="6846b-177">b.</span><span class="sxs-lookup"><span data-stu-id="6846b-177">b.</span></span> <span data-ttu-id="6846b-178">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6846b-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6846b-180">c.</span><span class="sxs-lookup"><span data-stu-id="6846b-180">c.</span></span> <span data-ttu-id="6846b-181">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6846b-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="6846b-182">d.</span><span class="sxs-lookup"><span data-stu-id="6846b-182">d.</span></span> <span data-ttu-id="6846b-183">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6846b-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="6846b-184">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6846b-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="6846b-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6846b-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6846b-188">Na **konfiguracji Moxtra** , kliknij przycisk **skonfigurować Moxtra** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6846b-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6846b-189">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6846b-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="6846b-191">W innym oknie przeglądarki należy zalogować się jako administrator do witryny firmy Moxtra.</span><span class="sxs-lookup"><span data-stu-id="6846b-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="6846b-192">Na pasku narzędzi po lewej stronie kliknij **konsoli administracyjnej > SAML logowania jednokrotnego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="6846b-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="6846b-194">Na **SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6846b-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="6846b-196">a.</span><span class="sxs-lookup"><span data-stu-id="6846b-196">a.</span></span> <span data-ttu-id="6846b-197">W **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="6846b-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="6846b-198">b.</span><span class="sxs-lookup"><span data-stu-id="6846b-198">b.</span></span> <span data-ttu-id="6846b-199">W **identyfikator jednostki IdP** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6846b-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6846b-200">c.</span><span class="sxs-lookup"><span data-stu-id="6846b-200">c.</span></span> <span data-ttu-id="6846b-201">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6846b-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6846b-202">d.</span><span class="sxs-lookup"><span data-stu-id="6846b-202">d.</span></span> <span data-ttu-id="6846b-203">W **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="6846b-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="6846b-204">e.</span><span class="sxs-lookup"><span data-stu-id="6846b-204">e.</span></span> <span data-ttu-id="6846b-205">W **NameID Format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="6846b-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="6846b-206">f.</span><span class="sxs-lookup"><span data-stu-id="6846b-206">f.</span></span> <span data-ttu-id="6846b-207">Otwórz certyfikat, który został pobrany z portalu Azure w programie Notatnik, skopiuj zawartość, a następnie wklej go do **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="6846b-208">g.</span><span class="sxs-lookup"><span data-stu-id="6846b-208">g.</span></span> <span data-ttu-id="6846b-209">W polu tekstowym SAML domeny poczty e-mail wpisz domenę poczty e-mail SAML.</span><span class="sxs-lookup"><span data-stu-id="6846b-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="6846b-210">Aby zobaczyć kroki, aby zweryfikować domeny, kliknij przycisk "**i**" poniżej.</span><span class="sxs-lookup"><span data-stu-id="6846b-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="6846b-211">h.</span><span class="sxs-lookup"><span data-stu-id="6846b-211">h.</span></span> <span data-ttu-id="6846b-212">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="6846b-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="6846b-213">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6846b-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6846b-214">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6846b-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6846b-215">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6846b-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6846b-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6846b-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="6846b-217">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6846b-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6846b-219">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6846b-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6846b-220">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6846b-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6846b-222">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6846b-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6846b-224">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6846b-226">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6846b-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6846b-228">a.</span><span class="sxs-lookup"><span data-stu-id="6846b-228">a.</span></span> <span data-ttu-id="6846b-229">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6846b-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6846b-230">b.</span><span class="sxs-lookup"><span data-stu-id="6846b-230">b.</span></span> <span data-ttu-id="6846b-231">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6846b-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6846b-232">c.</span><span class="sxs-lookup"><span data-stu-id="6846b-232">c.</span></span> <span data-ttu-id="6846b-233">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6846b-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6846b-234">d.</span><span class="sxs-lookup"><span data-stu-id="6846b-234">d.</span></span> <span data-ttu-id="6846b-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6846b-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="6846b-236">Tworzenie użytkownika testowego Moxtra</span><span class="sxs-lookup"><span data-stu-id="6846b-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="6846b-237">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Moxtra.</span><span class="sxs-lookup"><span data-stu-id="6846b-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="6846b-238">**Aby utworzyć użytkownika o nazwie Simona Britta w Moxtra, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6846b-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6846b-239">Zalogować się do witryny firmy Moxtra jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6846b-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="6846b-240">Na pasku narzędzi po lewej stronie kliknij **konsoli administracyjnej > Zarządzanie użytkownikami**, a następnie **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6846b-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="6846b-242">Na **Dodaj użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6846b-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="6846b-243">a.</span><span class="sxs-lookup"><span data-stu-id="6846b-243">a.</span></span> <span data-ttu-id="6846b-244">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6846b-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="6846b-245">b.</span><span class="sxs-lookup"><span data-stu-id="6846b-245">b.</span></span> <span data-ttu-id="6846b-246">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="6846b-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="6846b-247">c.</span><span class="sxs-lookup"><span data-stu-id="6846b-247">c.</span></span> <span data-ttu-id="6846b-248">W **E-mail** tekstowym, wpisz adres e-mail firmy Britta identyczny z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6846b-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="6846b-249">d.</span><span class="sxs-lookup"><span data-stu-id="6846b-249">d.</span></span> <span data-ttu-id="6846b-250">W **dzielenia** pole tekstowe, typ **deweloperów**.</span><span class="sxs-lookup"><span data-stu-id="6846b-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="6846b-251">e.</span><span class="sxs-lookup"><span data-stu-id="6846b-251">e.</span></span> <span data-ttu-id="6846b-252">W **działu** pole tekstowe, typ **IT**.</span><span class="sxs-lookup"><span data-stu-id="6846b-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="6846b-253">f.</span><span class="sxs-lookup"><span data-stu-id="6846b-253">f.</span></span> <span data-ttu-id="6846b-254">Wybierz **administratora**.</span><span class="sxs-lookup"><span data-stu-id="6846b-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="6846b-255">g.</span><span class="sxs-lookup"><span data-stu-id="6846b-255">g.</span></span> <span data-ttu-id="6846b-256">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6846b-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6846b-257">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6846b-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6846b-258">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Moxtra.</span><span class="sxs-lookup"><span data-stu-id="6846b-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6846b-260">**Aby przypisać Simona Britta Moxtra, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6846b-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6846b-261">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6846b-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6846b-263">Na liście aplikacji zaznacz **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="6846b-263">In the applications list, select **Moxtra**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="6846b-265">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6846b-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6846b-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6846b-267">Click **Add** button.</span></span> <span data-ttu-id="6846b-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6846b-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6846b-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6846b-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6846b-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6846b-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6846b-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6846b-273">Testing single sign-on</span></span>

<span data-ttu-id="6846b-274">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6846b-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6846b-275">Po kliknięciu kafelka Moxtra w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Moxtra.</span><span class="sxs-lookup"><span data-stu-id="6846b-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="6846b-276">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6846b-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6846b-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6846b-277">Additional resources</span></span>

* [<span data-ttu-id="6846b-278">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6846b-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6846b-279">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6846b-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

