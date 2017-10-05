---
title: "Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługę TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="0f813-103">Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="0f813-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="0f813-104">W tym samouczku Dowiedz się jak zintegrować usługę TINFOIL SECURITY w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f813-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f813-105">Integracja z usługą Azure AD usługę TINFOIL SECURITY zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0f813-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0f813-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługę TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="0f813-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="0f813-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do usługę TINFOIL SECURITY (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f813-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f813-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0f813-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0f813-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f813-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f813-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f813-110">Prerequisites</span></span>

<span data-ttu-id="0f813-111">Aby skonfigurować integrację usługi Azure AD przy użyciu usługi TINFOIL SECURITY, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0f813-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="0f813-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f813-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f813-113">Usługa TINFOIL SECURITY logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0f813-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f813-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0f813-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f813-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0f813-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f813-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0f813-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f813-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f813-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f813-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0f813-118">Scenario description</span></span>
<span data-ttu-id="0f813-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0f813-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f813-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0f813-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f813-121">Dodaj usługę TINFOIL SECURITY z galerii</span><span class="sxs-lookup"><span data-stu-id="0f813-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="0f813-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f813-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="0f813-123">Dodaj usługę TINFOIL SECURITY z galerii</span><span class="sxs-lookup"><span data-stu-id="0f813-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="0f813-124">Aby skonfigurować integrację usługi Azure AD usługę TINFOIL SECURITY, należy dodać usługę TINFOIL SECURITY z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0f813-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0f813-125">**Aby dodać usługę TINFOIL SECURITY z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0f813-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0f813-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f813-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0f813-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0f813-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0f813-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f813-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0f813-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0f813-133">W polu wyszukiwania wpisz **usługę TINFOIL SECURITY**, wybierz pozycję **usługę TINFOIL SECURITY** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="0f813-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![Usługa TINFOIL SECURITY z galerii](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0f813-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f813-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0f813-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługę TINFOIL SECURITY w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f813-137">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić odpowiednikiem użytkownika na usługę TINFOIL SECURITY dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f813-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="0f813-138">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="0f813-139">Usługa TINFOIL SECURITY przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="0f813-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0f813-140">Aby skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="0f813-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0f813-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f813-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0f813-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f813-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f813-143">**[Tworzenie użytkownika testowego usługę TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta usługę TINFOIL SECURITY, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f813-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f813-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0f813-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f813-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="0f813-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0f813-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f813-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0f813-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="0f813-148">**Aby skonfigurować usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0f813-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="0f813-149">W portalu Azure na **usługę TINFOIL SECURITY** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0f813-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0f813-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="0f813-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML na podstawie logowania jednokrotnego](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="0f813-153">Na **TINFOIL SECURITY domeny i adres URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="0f813-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="0f813-155">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartość.</span><span class="sxs-lookup"><span data-stu-id="0f813-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="0f813-157">Aby dodać mapowania wymaganego atrybutu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f813-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="0f813-158">![Atrybuty](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0f813-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="0f813-159">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="0f813-159">Attribute Name</span></span>    |   <span data-ttu-id="0f813-160">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="0f813-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="0f813-161">AccountID</span><span class="sxs-lookup"><span data-stu-id="0f813-161">accountid</span></span> | <span data-ttu-id="0f813-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="0f813-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="0f813-163">a.</span><span class="sxs-lookup"><span data-stu-id="0f813-163">a.</span></span> <span data-ttu-id="0f813-164">Kliknij przycisk **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0f813-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="0f813-165">![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0f813-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="0f813-166">![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0f813-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="0f813-167">b.</span><span class="sxs-lookup"><span data-stu-id="0f813-167">b.</span></span> <span data-ttu-id="0f813-168">W **nazwa atrybutu** pole tekstowe, typ **accountid**.</span><span class="sxs-lookup"><span data-stu-id="0f813-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="0f813-169">c.</span><span class="sxs-lookup"><span data-stu-id="0f813-169">c.</span></span> <span data-ttu-id="0f813-170">W **wartość atrybutu** pole tekstowe, wklej identyfikator konta wartość, która zostanie wyświetlony później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="0f813-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="0f813-171">d.</span><span class="sxs-lookup"><span data-stu-id="0f813-171">d.</span></span> <span data-ttu-id="0f813-172">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f813-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="0f813-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f813-173">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0f813-175">Na **TINFOIL SECURITY Configuration** kliknij **skonfigurować usługę TINFOIL SECURITY** otworzyć **konfigurowania rejestracji** okna.</span><span class="sxs-lookup"><span data-stu-id="0f813-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0f813-176">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0f813-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja zabezpieczeń TINFOIL](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="0f813-178">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy usługę TINFOIL SECURITY jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0f813-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="0f813-179">Na pasku narzędzi u góry kliknij **Moje konto**.</span><span class="sxs-lookup"><span data-stu-id="0f813-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="0f813-180">![Pulpit nawigacyjny](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "pulpitu nawigacyjnego")</span><span class="sxs-lookup"><span data-stu-id="0f813-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="0f813-181">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="0f813-181">Click **Security**.</span></span>
   
    <span data-ttu-id="0f813-182">![Zabezpieczenia](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="0f813-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="0f813-183">Na **rejestracji jednokrotnej** konfiguracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f813-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="0f813-184">![Logowanie jednokrotne](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="0f813-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="0f813-185">a.</span><span class="sxs-lookup"><span data-stu-id="0f813-185">a.</span></span> <span data-ttu-id="0f813-186">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="0f813-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="0f813-187">b.</span><span class="sxs-lookup"><span data-stu-id="0f813-187">b.</span></span> <span data-ttu-id="0f813-188">Kliknij przycisk **ręcznej konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="0f813-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="0f813-189">c.</span><span class="sxs-lookup"><span data-stu-id="0f813-189">c.</span></span> <span data-ttu-id="0f813-190">W **adresu URL przesyłania SAML** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0f813-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="0f813-191">d.</span><span class="sxs-lookup"><span data-stu-id="0f813-191">d.</span></span> <span data-ttu-id="0f813-192">W **odcisk palca certyfikatu SAML** pole tekstowe, Wklej wartość **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0f813-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="0f813-193">e.</span><span class="sxs-lookup"><span data-stu-id="0f813-193">e.</span></span> <span data-ttu-id="0f813-194">Kopiuj **swój identyfikator konta** i Wklej wartość w **wartość atrybutu** pole tekstowe, w obszarze **Dodawanie atrybutu** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f813-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="0f813-195">f.</span><span class="sxs-lookup"><span data-stu-id="0f813-195">f.</span></span> <span data-ttu-id="0f813-196">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0f813-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0f813-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="0f813-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0f813-198">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="0f813-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0f813-199">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f813-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0f813-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f813-200">Create an Azure AD test user</span></span>
<span data-ttu-id="0f813-201">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f813-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0f813-203">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0f813-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0f813-204">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f813-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f813-206">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0f813-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="0f813-207">Użytkownicy i grupy -> Wszyscy użytkownicy</span><span class="sxs-lookup"><span data-stu-id="0f813-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f813-208">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Użytkownik](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f813-210">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f813-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f813-212">a.</span><span class="sxs-lookup"><span data-stu-id="0f813-212">a.</span></span> <span data-ttu-id="0f813-213">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f813-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f813-214">b.</span><span class="sxs-lookup"><span data-stu-id="0f813-214">b.</span></span> <span data-ttu-id="0f813-215">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0f813-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f813-216">c.</span><span class="sxs-lookup"><span data-stu-id="0f813-216">c.</span></span> <span data-ttu-id="0f813-217">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0f813-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0f813-218">d.</span><span class="sxs-lookup"><span data-stu-id="0f813-218">d.</span></span> <span data-ttu-id="0f813-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f813-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="0f813-220">Tworzenie użytkownika testowego usługę TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="0f813-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="0f813-221">Aby włączyć użytkowników usługi Azure AD zalogować się do usługę TINFOIL SECURITY, musi być przygotowana do usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="0f813-222">W przypadku usługę TINFOIL SECURITY Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="0f813-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="0f813-223">**Aby uzyskać dostęp użytkownik zainicjowano obsługę administracyjną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0f813-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="0f813-224">Jeśli użytkownik jest część konta organizacji, musisz [skontaktuj się z zespołem pomocy technicznej usługę TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) uzyskać konto użytkownika utworzone.</span><span class="sxs-lookup"><span data-stu-id="0f813-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="0f813-225">Jeśli użytkownik jest zwykłych użytkowników TINFOIL SECURITY SaaS, użytkownik może dodawać współpracownika dla każdego użytkownika witryny.</span><span class="sxs-lookup"><span data-stu-id="0f813-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="0f813-226">Spowoduje to zainicjowanie procesu, aby wysłać zaproszenie na określony adres e-mail, aby utworzyć nowe konto użytkownika usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="0f813-227">Inne narzędzia do tworzenia konta użytkownika usługę TINFOIL SECURITY lub interfejsów API dostarczonych przez usługę TINFOIL SECURITY służy do obsługi administracyjnej kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f813-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0f813-228">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f813-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="0f813-229">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0f813-231">**Aby przypisać Simona Britta usługę TINFOIL SECURITY, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0f813-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="0f813-232">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f813-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0f813-234">Na liście aplikacji zaznacz **usługę TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="0f813-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![Wybierz usługę TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="0f813-236">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0f813-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0f813-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f813-238">Click **Add** button.</span></span> <span data-ttu-id="0f813-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0f813-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="0f813-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0f813-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f813-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f813-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0f813-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f813-244">Test single sign-on</span></span>

<span data-ttu-id="0f813-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0f813-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0f813-246">Po kliknięciu kafelka usługę TINFOIL SECURITY w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługę TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="0f813-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="0f813-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f813-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f813-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0f813-248">Additional resources</span></span>

* [<span data-ttu-id="0f813-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f813-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f813-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f813-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

