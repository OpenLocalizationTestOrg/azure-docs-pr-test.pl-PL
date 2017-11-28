---
title: 'Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SkyDesk wiadomości E-mail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="541ed-103">Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="541ed-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="541ed-104">Z tego samouczka dowiesz się integrowanie SkyDesk poczty E-mail w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="541ed-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="541ed-105">Integrowanie SkyDesk wiadomości E-mail z usługi Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="541ed-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="541ed-106">Można kontrolować w usłudze Azure AD, który ma dostęp do poczty E-mail SkyDesk</span><span class="sxs-lookup"><span data-stu-id="541ed-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="541ed-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do poczty E-mail SkyDesk (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="541ed-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="541ed-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="541ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="541ed-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="541ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="541ed-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="541ed-110">Prerequisites</span></span>

<span data-ttu-id="541ed-111">Aby skonfigurować integrację usługi Azure AD z SkyDesk poczty E-mail, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="541ed-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="541ed-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="541ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="541ed-113">E-mail SkyDesk logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="541ed-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="541ed-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="541ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="541ed-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="541ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="541ed-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="541ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="541ed-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="541ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="541ed-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="541ed-118">Scenario description</span></span>
<span data-ttu-id="541ed-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="541ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="541ed-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="541ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="541ed-121">Dodawanie SkyDesk wiadomości E-mail z galerii</span><span class="sxs-lookup"><span data-stu-id="541ed-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="541ed-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="541ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="541ed-123">Dodawanie SkyDesk wiadomości E-mail z galerii</span><span class="sxs-lookup"><span data-stu-id="541ed-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="541ed-124">Aby skonfigurować integrację SkyDesk poczty e-mail w usłudze Azure Active Directory, należy dodać SkyDesk wiadomości E-mail z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="541ed-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="541ed-125">**Aby dodać SkyDesk wiadomości E-mail z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="541ed-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="541ed-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="541ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="541ed-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="541ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="541ed-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="541ed-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="541ed-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="541ed-133">W polu wyszukiwania wpisz **E-mail SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="541ed-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="541ed-135">W panelu wyników wybierz **E-mail SkyDesk**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="541ed-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="541ed-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="541ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="541ed-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="541ed-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w SkyDesk wiadomości E-mail do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="541ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="541ed-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w wiadomości E-mail SkyDesk musi się.</span><span class="sxs-lookup"><span data-stu-id="541ed-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="541ed-141">W wiadomości E-mail SkyDesk, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="541ed-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="541ed-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="541ed-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="541ed-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="541ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="541ed-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="541ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="541ed-145">**[Tworzenie użytkownika testowego E-mail SkyDesk](#creating-a-skydesk-email-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SkyDesk wiadomości E-mail, jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="541ed-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="541ed-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="541ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="541ed-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="541ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="541ed-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="541ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="541ed-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji poczty E-mail SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="541ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="541ed-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="541ed-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="541ed-151">W portalu Azure na **E-mail SkyDesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="541ed-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="541ed-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="541ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="541ed-155">Na **SkyDesk domenę poczty E-mail i adresów URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="541ed-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="541ed-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="541ed-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="541ed-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="541ed-158">The value is not real.</span></span> <span data-ttu-id="541ed-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="541ed-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="541ed-160">Skontaktuj się z [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="541ed-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="541ed-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="541ed-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="541ed-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="541ed-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="541ed-165">Na **konfiguracji poczty E-mail SkyDesk** kliknij pozycję **konfigurowanie poczty E-mail SkyDesk** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="541ed-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="541ed-166">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="541ed-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="541ed-168">Aby włączyć logowanie Jednokrotne w **E-mail SkyDesk**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="541ed-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="541ed-169">a.</span><span class="sxs-lookup"><span data-stu-id="541ed-169">a.</span></span> <span data-ttu-id="541ed-170">Logowanie do konta E-mail SkyDesk jako administrator.</span><span class="sxs-lookup"><span data-stu-id="541ed-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="541ed-171">b.</span><span class="sxs-lookup"><span data-stu-id="541ed-171">b.</span></span> <span data-ttu-id="541ed-172">W menu u góry kliknij **Instalator**i wybierz **organizacji**.</span><span class="sxs-lookup"><span data-stu-id="541ed-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="541ed-174">c.</span><span class="sxs-lookup"><span data-stu-id="541ed-174">c.</span></span> <span data-ttu-id="541ed-175">Polecenie **domen** z lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="541ed-175">Click on **Domains** from the left panel.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="541ed-177">d.</span><span class="sxs-lookup"><span data-stu-id="541ed-177">d.</span></span> <span data-ttu-id="541ed-178">Polecenie **Dodawanie domeny**.</span><span class="sxs-lookup"><span data-stu-id="541ed-178">Click on **Add Domain**.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="541ed-180">e.</span><span class="sxs-lookup"><span data-stu-id="541ed-180">e.</span></span> <span data-ttu-id="541ed-181">Wpisz nazwę domeny, a następnie zweryfikować domenę.</span><span class="sxs-lookup"><span data-stu-id="541ed-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="541ed-183">f.</span><span class="sxs-lookup"><span data-stu-id="541ed-183">f.</span></span> <span data-ttu-id="541ed-184">Polecenie **uwierzytelnianie SAML** z lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="541ed-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="541ed-186">Na **uwierzytelnianie SAML** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="541ed-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="541ed-188">Aby używać uwierzytelniania na podstawie SAML, albo powinien mieć **zweryfikowaną domeną** lub **portal adresu URL** Instalatora.</span><span class="sxs-lookup"><span data-stu-id="541ed-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="541ed-189">Można ustawić portalu adres URL o unikatowej nazwie.</span><span class="sxs-lookup"><span data-stu-id="541ed-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="541ed-191">a.</span><span class="sxs-lookup"><span data-stu-id="541ed-191">a.</span></span> <span data-ttu-id="541ed-192">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="541ed-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="541ed-193">b.</span><span class="sxs-lookup"><span data-stu-id="541ed-193">b.</span></span> <span data-ttu-id="541ed-194">W **wylogowania** pole tekstowe adresu URL, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="541ed-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="541ed-195">c.</span><span class="sxs-lookup"><span data-stu-id="541ed-195">c.</span></span> <span data-ttu-id="541ed-196">**Zmień adres URL hasła** jest opcjonalny, dlatego pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="541ed-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="541ed-197">d.</span><span class="sxs-lookup"><span data-stu-id="541ed-197">d.</span></span> <span data-ttu-id="541ed-198">Polecenie **uzyskać klucz z pliku** wybierz certyfikat pobrany z portalu Azure, a następnie kliknij przycisk **Otwórz** można przekazać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="541ed-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="541ed-199">e.</span><span class="sxs-lookup"><span data-stu-id="541ed-199">e.</span></span> <span data-ttu-id="541ed-200">Jako **algorytm**, wybierz pozycję **RSA**.</span><span class="sxs-lookup"><span data-stu-id="541ed-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="541ed-201">f.</span><span class="sxs-lookup"><span data-stu-id="541ed-201">f.</span></span> <span data-ttu-id="541ed-202">Kliknij przycisk **Ok** Aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="541ed-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="541ed-203">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="541ed-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="541ed-204">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="541ed-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="541ed-205">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="541ed-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="541ed-206">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="541ed-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="541ed-207">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="541ed-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="541ed-209">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="541ed-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="541ed-210">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="541ed-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="541ed-212">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="541ed-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="541ed-214">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="541ed-216">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="541ed-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="541ed-218">a.</span><span class="sxs-lookup"><span data-stu-id="541ed-218">a.</span></span> <span data-ttu-id="541ed-219">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="541ed-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="541ed-220">b.</span><span class="sxs-lookup"><span data-stu-id="541ed-220">b.</span></span> <span data-ttu-id="541ed-221">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="541ed-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="541ed-222">c.</span><span class="sxs-lookup"><span data-stu-id="541ed-222">c.</span></span> <span data-ttu-id="541ed-223">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="541ed-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="541ed-224">d.</span><span class="sxs-lookup"><span data-stu-id="541ed-224">d.</span></span> <span data-ttu-id="541ed-225">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="541ed-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="541ed-226">Tworzenie użytkownika testowego SkyDesk poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="541ed-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="541ed-227">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w SkyDesk wiadomości E-mail.</span><span class="sxs-lookup"><span data-stu-id="541ed-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="541ed-228">Polecenie **dostępu użytkownika** z lewym panelu w SkyDesk wiadomości E-mail, a następnie wprowadź nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="541ed-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="541ed-230">Jeśli musisz utworzyć zbiorczego użytkowników, należy skontaktować się [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="541ed-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="541ed-231">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="541ed-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="541ed-232">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do poczty E-mail SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="541ed-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="541ed-234">**Aby przypisać Simona Britta SkyDesk poczty E-mail, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="541ed-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="541ed-235">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="541ed-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="541ed-237">Na liście aplikacji zaznacz **E-mail SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="541ed-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="541ed-239">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="541ed-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="541ed-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="541ed-241">Click **Add** button.</span></span> <span data-ttu-id="541ed-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="541ed-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="541ed-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="541ed-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="541ed-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="541ed-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="541ed-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="541ed-247">Testing single sign-on</span></span>

<span data-ttu-id="541ed-248">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="541ed-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="541ed-249">Po kliknięciu kafelka SkyDesk poczty E-mail w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji poczty E-mail SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="541ed-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="541ed-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="541ed-250">Additional resources</span></span>

* [<span data-ttu-id="541ed-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="541ed-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="541ed-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="541ed-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

