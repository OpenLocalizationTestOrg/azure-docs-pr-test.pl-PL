---
title: 'Samouczek: Integracji Azure Active Directory z elementami SD | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i elementy SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="106d4-103">Samouczek: Integracji Azure Active Directory z elementami SD.</span><span class="sxs-lookup"><span data-stu-id="106d4-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="106d4-104">Z tego samouczka dowiesz integrowanie SD elementy z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="106d4-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="106d4-105">Integrowanie SD elementy z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="106d4-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="106d4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do elementów SD.</span><span class="sxs-lookup"><span data-stu-id="106d4-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="106d4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane elementy SD (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="106d4-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="106d4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="106d4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="106d4-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="106d4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="106d4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="106d4-110">Prerequisites</span></span>

<span data-ttu-id="106d4-111">Aby skonfigurować integrację usługi Azure AD z elementami SD, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="106d4-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="106d4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="106d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="106d4-113">Elementy SD logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="106d4-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="106d4-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="106d4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="106d4-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="106d4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="106d4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="106d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="106d4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="106d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="106d4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="106d4-118">Scenario description</span></span>
<span data-ttu-id="106d4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="106d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="106d4-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="106d4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="106d4-121">Dodawanie elementów SD z galerii</span><span class="sxs-lookup"><span data-stu-id="106d4-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="106d4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="106d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="106d4-123">Dodawanie elementów SD z galerii</span><span class="sxs-lookup"><span data-stu-id="106d4-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="106d4-124">Aby skonfigurować integrację usługi Azure AD elementy SD, należy dodać SD elementów z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="106d4-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="106d4-125">**Aby dodać SD elementów z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="106d4-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="106d4-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="106d4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="106d4-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="106d4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="106d4-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="106d4-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="106d4-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="106d4-133">W polu wyszukiwania wpisz **elementy SD**.</span><span class="sxs-lookup"><span data-stu-id="106d4-133">In the search box, type **SD Elements**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="106d4-135">W panelu wyników wybierz **elementy SD**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="106d4-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="106d4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="106d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="106d4-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z elementami SD, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="106d4-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w elementach SD jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="106d4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="106d4-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w elementach SD musi się.</span><span class="sxs-lookup"><span data-stu-id="106d4-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="106d4-141">W elementach SD, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="106d4-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="106d4-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z elementami SD, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="106d4-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="106d4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="106d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="106d4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="106d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="106d4-145">**[Tworzenie użytkownika testowego elementy SD](#creating-a-sd-elements-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta elementy SD, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="106d4-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="106d4-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="106d4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="106d4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="106d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="106d4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="106d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="106d4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SD elementów.</span><span class="sxs-lookup"><span data-stu-id="106d4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="106d4-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z elementami SD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="106d4-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="106d4-151">W portalu Azure na **elementy SD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="106d4-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="106d4-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="106d4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="106d4-155">Na **SD elementy domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="106d4-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="106d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="106d4-157">a.</span></span> <span data-ttu-id="106d4-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="106d4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="106d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="106d4-159">b.</span></span> <span data-ttu-id="106d4-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="106d4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="106d4-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="106d4-161">These values are not real.</span></span> <span data-ttu-id="106d4-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="106d4-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="106d4-163">Skontaktuj się z [elementy SD obsługują zespołu](mailto:support@sdelements.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="106d4-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="106d4-164">Elementy SD aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="106d4-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="106d4-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="106d4-165">Configure the following claims for this application.</span></span> <span data-ttu-id="106d4-166">Możesz zarządzać wartości tych atrybutów z **"Użytkownika atrybutu"** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="106d4-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="106d4-167">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="106d4-167">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="106d4-169">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="106d4-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="106d4-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="106d4-170">Attribute Name</span></span> | <span data-ttu-id="106d4-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="106d4-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="106d4-172">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="106d4-172">email</span></span> |<span data-ttu-id="106d4-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="106d4-173">user.mail</span></span> |
    | <span data-ttu-id="106d4-174">Imię</span><span class="sxs-lookup"><span data-stu-id="106d4-174">firstname</span></span> |<span data-ttu-id="106d4-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="106d4-175">user.givenname</span></span> |
    | <span data-ttu-id="106d4-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="106d4-176">lastname</span></span> |<span data-ttu-id="106d4-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="106d4-177">user.surname</span></span> |

    <span data-ttu-id="106d4-178">a.</span><span class="sxs-lookup"><span data-stu-id="106d4-178">a.</span></span> <span data-ttu-id="106d4-179">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="106d4-182">b.</span><span class="sxs-lookup"><span data-stu-id="106d4-182">b.</span></span> <span data-ttu-id="106d4-183">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="106d4-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="106d4-184">c.</span><span class="sxs-lookup"><span data-stu-id="106d4-184">c.</span></span> <span data-ttu-id="106d4-185">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="106d4-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="106d4-186">d.</span><span class="sxs-lookup"><span data-stu-id="106d4-186">d.</span></span> <span data-ttu-id="106d4-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="106d4-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="106d4-188">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="106d4-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="106d4-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="106d4-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="106d4-192">Na **SD elementy konfiguracji** kliknij **skonfigurować elementy SD** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="106d4-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="106d4-193">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="106d4-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="106d4-195">Aby uzyskać logowanie jednokrotne włączone, skontaktuj się z Twojej [elementy SD obsługują team](mailto:support@sdelements.com) i udostępnia je z pliku pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="106d4-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="106d4-196">W oknie innej przeglądarki logowanie do dzierżawy SD elementów jako administrator.</span><span class="sxs-lookup"><span data-stu-id="106d4-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="106d4-197">W menu u góry kliknij **systemu**, a następnie **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="106d4-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="106d4-199">Na **ustawień rejestracji jednokrotnej** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="106d4-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="106d4-201">a.</span><span class="sxs-lookup"><span data-stu-id="106d4-201">a.</span></span> <span data-ttu-id="106d4-202">Jako **typ logowania jednokrotnego**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="106d4-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="106d4-203">b.</span><span class="sxs-lookup"><span data-stu-id="106d4-203">b.</span></span> <span data-ttu-id="106d4-204">W **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="106d4-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="106d4-205">c.</span><span class="sxs-lookup"><span data-stu-id="106d4-205">c.</span></span> <span data-ttu-id="106d4-206">W **Dostawca pojedynczego logowania jednokrotnego usługi tożsamości** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="106d4-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="106d4-207">d.</span><span class="sxs-lookup"><span data-stu-id="106d4-207">d.</span></span> <span data-ttu-id="106d4-208">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="106d4-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="106d4-209">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="106d4-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="106d4-210">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="106d4-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="106d4-211">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="106d4-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="106d4-212">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="106d4-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="106d4-213">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="106d4-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="106d4-215">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="106d4-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="106d4-216">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="106d4-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="106d4-218">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="106d4-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="106d4-220">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="106d4-222">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="106d4-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="106d4-224">a.</span><span class="sxs-lookup"><span data-stu-id="106d4-224">a.</span></span> <span data-ttu-id="106d4-225">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="106d4-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="106d4-226">b.</span><span class="sxs-lookup"><span data-stu-id="106d4-226">b.</span></span> <span data-ttu-id="106d4-227">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="106d4-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="106d4-228">c.</span><span class="sxs-lookup"><span data-stu-id="106d4-228">c.</span></span> <span data-ttu-id="106d4-229">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="106d4-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="106d4-230">d.</span><span class="sxs-lookup"><span data-stu-id="106d4-230">d.</span></span> <span data-ttu-id="106d4-231">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="106d4-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="106d4-232">Tworzenie użytkownika testowego elementy SD.</span><span class="sxs-lookup"><span data-stu-id="106d4-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="106d4-233">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta SD elementów.</span><span class="sxs-lookup"><span data-stu-id="106d4-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="106d4-234">W przypadku elementów SD tworzenie elementów SD użytkowników jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="106d4-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="106d4-235">**Aby utworzyć Simona Britta w elementach SD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="106d4-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="106d4-236">W oknie przeglądarki sieci web logowania do witryny firmy SD elementów jako administrator.</span><span class="sxs-lookup"><span data-stu-id="106d4-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="106d4-237">W menu u góry kliknij **Zarządzanie użytkownikami**, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="106d4-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="106d4-239">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="106d4-239">Click **Add New User**.</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="106d4-241">Na **Dodaj nowego użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="106d4-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="106d4-243">a.</span><span class="sxs-lookup"><span data-stu-id="106d4-243">a.</span></span> <span data-ttu-id="106d4-244">W **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="106d4-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="106d4-245">b.</span><span class="sxs-lookup"><span data-stu-id="106d4-245">b.</span></span> <span data-ttu-id="106d4-246">W **imię** pole tekstowe, wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="106d4-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="106d4-247">c.</span><span class="sxs-lookup"><span data-stu-id="106d4-247">c.</span></span> <span data-ttu-id="106d4-248">W **nazwisko** pole tekstowe, wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="106d4-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="106d4-249">d.</span><span class="sxs-lookup"><span data-stu-id="106d4-249">d.</span></span> <span data-ttu-id="106d4-250">Jako **roli**, wybierz pozycję **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="106d4-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="106d4-251">e.</span><span class="sxs-lookup"><span data-stu-id="106d4-251">e.</span></span> <span data-ttu-id="106d4-252">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="106d4-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="106d4-253">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="106d4-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="106d4-254">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do elementów SD.</span><span class="sxs-lookup"><span data-stu-id="106d4-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="106d4-256">**Aby przypisać Simona Britta elementy SD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="106d4-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="106d4-257">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="106d4-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="106d4-259">Na liście aplikacji zaznacz **elementy SD**.</span><span class="sxs-lookup"><span data-stu-id="106d4-259">In the applications list, select **SD Elements**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="106d4-261">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="106d4-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="106d4-263">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="106d4-263">Click **Add** button.</span></span> <span data-ttu-id="106d4-264">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="106d4-266">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="106d4-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="106d4-267">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="106d4-268">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="106d4-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="106d4-269">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="106d4-269">Testing single sign-on</span></span>

<span data-ttu-id="106d4-270">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="106d4-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="106d4-271">Po kliknięciu kafelka SD elementów w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji SD elementów.</span><span class="sxs-lookup"><span data-stu-id="106d4-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="106d4-272">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="106d4-272">Additional resources</span></span>

* [<span data-ttu-id="106d4-273">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="106d4-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="106d4-274">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="106d4-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

