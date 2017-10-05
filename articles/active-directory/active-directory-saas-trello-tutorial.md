---
title: 'Samouczek: Integracji Azure Active Directory z Trello | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="542e9-103">Samouczek: Integracji Azure Active Directory z Trello</span><span class="sxs-lookup"><span data-stu-id="542e9-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="542e9-104">Z tego samouczka dowiesz się integrowanie Trello z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="542e9-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="542e9-105">Integracja z usługą Azure AD Trello zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="542e9-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="542e9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Trello</span><span class="sxs-lookup"><span data-stu-id="542e9-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="542e9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Trello (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="542e9-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="542e9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="542e9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="542e9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="542e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="542e9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="542e9-110">Prerequisites</span></span>

<span data-ttu-id="542e9-111">Aby skonfigurować integrację usługi Azure AD z Trello, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="542e9-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="542e9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="542e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="542e9-113">Trello logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="542e9-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="542e9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="542e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="542e9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="542e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="542e9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="542e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="542e9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="542e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="542e9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="542e9-118">Scenario description</span></span>
<span data-ttu-id="542e9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="542e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="542e9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="542e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="542e9-121">Dodawanie Trello z galerii</span><span class="sxs-lookup"><span data-stu-id="542e9-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="542e9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="542e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="542e9-123">Dodawanie Trello z galerii</span><span class="sxs-lookup"><span data-stu-id="542e9-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="542e9-124">Aby skonfigurować integrację usługi Azure AD Trello, należy dodać Trello z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="542e9-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="542e9-125">**Aby dodać Trello z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="542e9-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="542e9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="542e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="542e9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="542e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="542e9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="542e9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="542e9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="542e9-133">W polu wyszukiwania wpisz **Trello**.</span><span class="sxs-lookup"><span data-stu-id="542e9-133">In the search box, type **Trello**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="542e9-135">W panelu wyników wybierz **Trello**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="542e9-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="542e9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="542e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="542e9-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Trello w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="542e9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Trello jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="542e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="542e9-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Trello musi się.</span><span class="sxs-lookup"><span data-stu-id="542e9-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="542e9-141">W Trello, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="542e9-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="542e9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Trello, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="542e9-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="542e9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="542e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="542e9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="542e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="542e9-145">**[Tworzenie użytkownika testowego Trello](#creating-a-trello-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Trello połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="542e9-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="542e9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="542e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="542e9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="542e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="542e9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="542e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="542e9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="542e9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Trello, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="542e9-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="542e9-151">W portalu Azure na **Trello** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="542e9-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="542e9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="542e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="542e9-155">Na **Trello domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="542e9-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="542e9-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="542e9-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="542e9-158">Na **Trello domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="542e9-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="542e9-160">a.</span><span class="sxs-lookup"><span data-stu-id="542e9-160">a.</span></span> <span data-ttu-id="542e9-161">Polecenie **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="542e9-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="542e9-162">b.</span><span class="sxs-lookup"><span data-stu-id="542e9-162">b.</span></span> <span data-ttu-id="542e9-163">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="542e9-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="542e9-164">Należy pobrać  **\<enterprise\>**  informacji o pracy z Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="542e9-165">Jeśli nie masz wartość informacji o pracy, skontaktuj się z [zespołem pomocy technicznej Trello](mailto:support@trello.com) można uzyskać informacji o pracy należy przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="542e9-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="542e9-166">Aplikacja Trello oczekuje potwierdzenia SAML w celu uwzględnienia określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="542e9-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="542e9-167">Skonfiguruj następujące atrybuty dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="542e9-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="542e9-168">Możesz zarządzać wartości tych atrybutów z **"Atrybuty użytkownika"** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="542e9-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="542e9-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="542e9-169">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="542e9-171">Na **atrybuty tokenu SAML** okna dialogowego, dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="542e9-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="542e9-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="542e9-172">Attribute Name</span></span> | <span data-ttu-id="542e9-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="542e9-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="542e9-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="542e9-174">User.Email</span></span> | <span data-ttu-id="542e9-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="542e9-175">user.mail</span></span> |
    | <span data-ttu-id="542e9-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="542e9-176">User.FirstName</span></span> | <span data-ttu-id="542e9-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="542e9-177">user.givenname</span></span> |
    | <span data-ttu-id="542e9-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="542e9-178">User.LastName</span></span> | <span data-ttu-id="542e9-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="542e9-179">user.surname</span></span> |

    <span data-ttu-id="542e9-180">a.</span><span class="sxs-lookup"><span data-stu-id="542e9-180">a.</span></span> <span data-ttu-id="542e9-181">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="542e9-184">b.</span><span class="sxs-lookup"><span data-stu-id="542e9-184">b.</span></span> <span data-ttu-id="542e9-185">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="542e9-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="542e9-186">c.</span><span class="sxs-lookup"><span data-stu-id="542e9-186">c.</span></span> <span data-ttu-id="542e9-187">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="542e9-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="542e9-188">d.</span><span class="sxs-lookup"><span data-stu-id="542e9-188">d.</span></span> <span data-ttu-id="542e9-189">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="542e9-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="542e9-190">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="542e9-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="542e9-192">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="542e9-192">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="542e9-194">Na **konfiguracji Trello** , kliknij przycisk **skonfigurować Trello** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="542e9-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="542e9-195">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="542e9-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="542e9-197">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, przejdź do [konfiguracji logowania jednokrotnego przedsiębiorstwa Trello](https://trello.com/sso-configuration) stronę, aby wysłać [zespołem pomocy technicznej Trello](mailto:support@trello.com) **SAML pojedynczy znak na adres URL usługi** i Dołącz **certyfikatu (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="542e9-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="542e9-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="542e9-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="542e9-199">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="542e9-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="542e9-200">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="542e9-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="542e9-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="542e9-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="542e9-202">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="542e9-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="542e9-204">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="542e9-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="542e9-205">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="542e9-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="542e9-207">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="542e9-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="542e9-209">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="542e9-211">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="542e9-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="542e9-213">a.</span><span class="sxs-lookup"><span data-stu-id="542e9-213">a.</span></span> <span data-ttu-id="542e9-214">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="542e9-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="542e9-215">b.</span><span class="sxs-lookup"><span data-stu-id="542e9-215">b.</span></span> <span data-ttu-id="542e9-216">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="542e9-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="542e9-217">c.</span><span class="sxs-lookup"><span data-stu-id="542e9-217">c.</span></span> <span data-ttu-id="542e9-218">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="542e9-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="542e9-219">d.</span><span class="sxs-lookup"><span data-stu-id="542e9-219">d.</span></span> <span data-ttu-id="542e9-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="542e9-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="542e9-221">Tworzenie użytkownika testowego Trello</span><span class="sxs-lookup"><span data-stu-id="542e9-221">Creating a Trello test user</span></span>

<span data-ttu-id="542e9-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="542e9-223">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="542e9-224">Trello obsługę w czasie i nowe konto jest tworzone podczas pierwszego logowania z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="542e9-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="542e9-225">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="542e9-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="542e9-226">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="542e9-228">**Aby przypisać Simona Britta Trello, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="542e9-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="542e9-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="542e9-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="542e9-231">Na liście aplikacji zaznacz **Trello**.</span><span class="sxs-lookup"><span data-stu-id="542e9-231">In the applications list, select **Trello**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="542e9-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="542e9-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="542e9-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="542e9-235">Click **Add** button.</span></span> <span data-ttu-id="542e9-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="542e9-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="542e9-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="542e9-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="542e9-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="542e9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="542e9-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="542e9-241">Testing single sign-on</span></span>

<span data-ttu-id="542e9-242">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="542e9-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="542e9-243">Po kliknięciu kafelka Trello w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Trello.</span><span class="sxs-lookup"><span data-stu-id="542e9-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="542e9-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="542e9-244">Additional resources</span></span>

* [<span data-ttu-id="542e9-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="542e9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="542e9-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="542e9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

