---
title: 'Samouczek: Integracji Azure Active Directory z zapas czasu | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i zapas czasu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="bccba-103">Samouczek: Integracji Azure Active Directory z zapas czasu</span><span class="sxs-lookup"><span data-stu-id="bccba-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="bccba-104">Z tego samouczka dowiesz się integrowanie zapas czasu w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bccba-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bccba-105">Integrowanie zapas czasu z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bccba-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bccba-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zapas czasu</span><span class="sxs-lookup"><span data-stu-id="bccba-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="bccba-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Slack (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bccba-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bccba-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bccba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bccba-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bccba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bccba-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bccba-110">Prerequisites</span></span>

<span data-ttu-id="bccba-111">Aby skonfigurować integrację usługi Azure AD z zapas czasu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bccba-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="bccba-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bccba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bccba-113">Slack logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bccba-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bccba-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bccba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bccba-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bccba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bccba-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bccba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bccba-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bccba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bccba-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bccba-118">Scenario description</span></span>
<span data-ttu-id="bccba-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bccba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bccba-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bccba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bccba-121">Dodawanie zapas czasu z galerii</span><span class="sxs-lookup"><span data-stu-id="bccba-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="bccba-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bccba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="bccba-123">Dodawanie zapas czasu z galerii</span><span class="sxs-lookup"><span data-stu-id="bccba-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="bccba-124">Aby skonfigurować integrację zapas czasu w usłudze Azure Active Directory, należy dodać zapas czasu z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bccba-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bccba-125">**Aby dodać zapas czasu z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bccba-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bccba-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bccba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bccba-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bccba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bccba-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bccba-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bccba-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bccba-133">W polu wyszukiwania wpisz **Slack**.</span><span class="sxs-lookup"><span data-stu-id="bccba-133">In the search box, type **Slack**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="bccba-135">W panelu wyników wybierz **Slack**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bccba-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bccba-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bccba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bccba-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zapas czasu, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bccba-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w zapas czasu jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bccba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="bccba-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w zapas czasu musi się.</span><span class="sxs-lookup"><span data-stu-id="bccba-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="bccba-141">W zapas czasu, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bccba-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bccba-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zapas czasu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bccba-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bccba-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bccba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bccba-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bccba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bccba-145">**[Tworzenie użytkownika testowego Slack](#creating-a-slack-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta zapas czasu połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bccba-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bccba-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bccba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bccba-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bccba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bccba-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bccba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bccba-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Slack.</span><span class="sxs-lookup"><span data-stu-id="bccba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="bccba-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z zapas czasu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bccba-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="bccba-151">W portalu Azure na **Slack** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bccba-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bccba-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bccba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="bccba-155">Na **domeny zapas czasu i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bccba-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="bccba-157">a.</span><span class="sxs-lookup"><span data-stu-id="bccba-157">a.</span></span> <span data-ttu-id="bccba-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="bccba-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="bccba-159">b.</span><span class="sxs-lookup"><span data-stu-id="bccba-159">b.</span></span> <span data-ttu-id="bccba-160">W **identyfikator** tekstowym, wpisz adres URL:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="bccba-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bccba-161">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bccba-161">The value is not real.</span></span> <span data-ttu-id="bccba-162">Należy zaktualizować wartości rzeczywistych logowania na adres URL.</span><span class="sxs-lookup"><span data-stu-id="bccba-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="bccba-163">Skontaktuj się z [zespołem pomocy technicznej Slack](https://slack.com/help/contact) można uzyskać wartość</span><span class="sxs-lookup"><span data-stu-id="bccba-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="bccba-164">Slack aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="bccba-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bccba-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bccba-165">Configure the following claims for this application.</span></span> <span data-ttu-id="bccba-166">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bccba-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bccba-167">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="bccba-167">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="bccba-169">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okno dialogowe, wybierz opcję **user.mail** jako **identyfikator użytkownika** i dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bccba-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="bccba-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="bccba-170">Attribute Name</span></span> | <span data-ttu-id="bccba-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="bccba-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bccba-172">Imię</span><span class="sxs-lookup"><span data-stu-id="bccba-172">first_name</span></span> | <span data-ttu-id="bccba-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="bccba-173">user.givenname</span></span> |
    | <span data-ttu-id="bccba-174">nazwisko</span><span class="sxs-lookup"><span data-stu-id="bccba-174">last_name</span></span> | <span data-ttu-id="bccba-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="bccba-175">user.surname</span></span> |
    | <span data-ttu-id="bccba-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="bccba-176">User.Email</span></span> | <span data-ttu-id="bccba-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="bccba-177">user.mail</span></span> |  
    | <span data-ttu-id="bccba-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="bccba-178">User.Username</span></span> | <span data-ttu-id="bccba-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="bccba-179">user.userprincipalname</span></span> |

    <span data-ttu-id="bccba-180">a.</span><span class="sxs-lookup"><span data-stu-id="bccba-180">a.</span></span> <span data-ttu-id="bccba-181">Polecenie **atrybutu** otworzyć **atrybutu Edytuj** okna dialogowego polu i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bccba-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="bccba-183">a.</span><span class="sxs-lookup"><span data-stu-id="bccba-183">a.</span></span> <span data-ttu-id="bccba-184">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bccba-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bccba-185">b.</span><span class="sxs-lookup"><span data-stu-id="bccba-185">b.</span></span> <span data-ttu-id="bccba-186">Z **wartość** listy, wybierz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bccba-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bccba-187">c.</span><span class="sxs-lookup"><span data-stu-id="bccba-187">c.</span></span> <span data-ttu-id="bccba-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bccba-188">Click **OK**</span></span>

6. <span data-ttu-id="bccba-189">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bccba-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="bccba-191">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bccba-191">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bccba-193">Na **konfiguracji zapas czasu** kliknij **skonfigurować zapas czasu** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bccba-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bccba-194">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bccba-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="bccba-196">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Slack.</span><span class="sxs-lookup"><span data-stu-id="bccba-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="bccba-197">Przejdź do **usługi Microsoft Azure AD** następnie przejdź do **ustawień zespołu**.</span><span class="sxs-lookup"><span data-stu-id="bccba-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="bccba-199">W **ustawień zespołu** kliknij **uwierzytelniania** , a następnie kliknij pozycję **Zmień ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="bccba-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="bccba-201">Na **ustawienia uwierzytelniania SAML** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bccba-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="bccba-203">a.</span><span class="sxs-lookup"><span data-stu-id="bccba-203">a.</span></span>  <span data-ttu-id="bccba-204">W **SAML 2.0 punktu końcowego (HTTP)** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bccba-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bccba-205">b.</span><span class="sxs-lookup"><span data-stu-id="bccba-205">b.</span></span>  <span data-ttu-id="bccba-206">W **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bccba-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bccba-207">c.</span><span class="sxs-lookup"><span data-stu-id="bccba-207">c.</span></span>  <span data-ttu-id="bccba-208">Otwórz w Notatniku plik certyfikatu pobrane, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu publicznego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="bccba-209">d.</span><span class="sxs-lookup"><span data-stu-id="bccba-209">d.</span></span> <span data-ttu-id="bccba-210">Skonfiguruj powyżej trzy ustawienia odpowiednie dla swojego zespołu Slack.</span><span class="sxs-lookup"><span data-stu-id="bccba-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="bccba-211">Aby uzyskać więcej informacji na temat ustawień znaleźć **Przewodnik po konfiguracji logowania jednokrotnego zapas czasu jego** tutaj.</span><span class="sxs-lookup"><span data-stu-id="bccba-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="bccba-212">e.</span><span class="sxs-lookup"><span data-stu-id="bccba-212">e.</span></span>  <span data-ttu-id="bccba-213">Kliknij przycisk **Zapisz konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="bccba-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="bccba-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bccba-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bccba-215">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bccba-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bccba-216">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bccba-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bccba-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bccba-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="bccba-218">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bccba-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bccba-220">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bccba-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bccba-221">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bccba-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bccba-223">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bccba-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bccba-225">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bccba-227">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bccba-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bccba-229">a.</span><span class="sxs-lookup"><span data-stu-id="bccba-229">a.</span></span> <span data-ttu-id="bccba-230">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bccba-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bccba-231">b.</span><span class="sxs-lookup"><span data-stu-id="bccba-231">b.</span></span> <span data-ttu-id="bccba-232">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bccba-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bccba-233">c.</span><span class="sxs-lookup"><span data-stu-id="bccba-233">c.</span></span> <span data-ttu-id="bccba-234">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bccba-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bccba-235">d.</span><span class="sxs-lookup"><span data-stu-id="bccba-235">d.</span></span> <span data-ttu-id="bccba-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bccba-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="bccba-237">Tworzenie użytkownika testowego Slack</span><span class="sxs-lookup"><span data-stu-id="bccba-237">Creating a Slack test user</span></span>

<span data-ttu-id="bccba-238">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Slack.</span><span class="sxs-lookup"><span data-stu-id="bccba-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="bccba-239">Zapas czasu obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="bccba-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bccba-240">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="bccba-240">There is no action item for you in this section.</span></span> <span data-ttu-id="bccba-241">Nowy użytkownik został utworzony podczas próby dostępu zapas czasu, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bccba-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="bccba-242">Jeśli trzeba ręcznie utworzyć użytkownika, należy nawiązać [zespołem pomocy technicznej Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="bccba-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bccba-243">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bccba-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bccba-244">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="bccba-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bccba-246">**Aby przypisać Simona Britta zapas czasu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bccba-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="bccba-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bccba-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bccba-249">Na liście aplikacji zaznacz **Slack**.</span><span class="sxs-lookup"><span data-stu-id="bccba-249">In the applications list, select **Slack**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="bccba-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bccba-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bccba-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bccba-253">Click **Add** button.</span></span> <span data-ttu-id="bccba-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bccba-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bccba-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bccba-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bccba-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bccba-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bccba-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bccba-259">Testing single sign-on</span></span>

<span data-ttu-id="bccba-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bccba-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bccba-261">Po kliknięciu kafelka Slack w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Slack aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bccba-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bccba-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bccba-262">Additional resources</span></span>

* [<span data-ttu-id="bccba-263">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bccba-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bccba-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bccba-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

