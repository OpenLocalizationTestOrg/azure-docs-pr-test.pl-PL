---
title: 'Samouczek: Integracji Azure Active Directory z AirWatch | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="7b4b9-103">Samouczek: Integracji Azure Active Directory z AirWatch</span><span class="sxs-lookup"><span data-stu-id="7b4b9-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="7b4b9-104">Z tego samouczka dowiesz się integrowanie AirWatch z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b4b9-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b4b9-105">Integracja z usługą Azure AD AirWatch zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b4b9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do AirWatch</span><span class="sxs-lookup"><span data-stu-id="7b4b9-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="7b4b9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do AirWatch (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b4b9-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b4b9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7b4b9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b4b9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b4b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b4b9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b4b9-110">Prerequisites</span></span>

<span data-ttu-id="7b4b9-111">Aby skonfigurować integrację usługi Azure AD z AirWatch, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="7b4b9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b4b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b4b9-113">AirWatch jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7b4b9-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b4b9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b4b9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b4b9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b4b9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b4b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b4b9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7b4b9-118">Scenario description</span></span>
<span data-ttu-id="7b4b9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b4b9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b4b9-121">Dodawanie AirWatch z galerii</span><span class="sxs-lookup"><span data-stu-id="7b4b9-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="7b4b9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7b4b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="7b4b9-123">Dodawanie AirWatch z galerii</span><span class="sxs-lookup"><span data-stu-id="7b4b9-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="7b4b9-124">Aby skonfigurować integrację usługi Azure AD AirWatch, należy dodać AirWatch z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b4b9-125">**Aby dodać AirWatch z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b4b9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7b4b9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b4b9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7b4b9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7b4b9-133">W polu wyszukiwania wpisz **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-133">In the search box, type **AirWatch**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="7b4b9-135">W panelu wyników wybierz **AirWatch**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b4b9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7b4b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b4b9-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AirWatch na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7b4b9-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b4b9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w AirWatch jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="7b4b9-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w AirWatch musi się.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="7b4b9-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w AirWatch.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="7b4b9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AirWatch, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b4b9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7b4b9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b4b9-145">**[Tworzenie użytkownika testowego AirWatch](#creating-a-airwatch-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta AirWatch połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b4b9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b4b9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b4b9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b4b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b4b9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji AirWatch.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="7b4b9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z AirWatch, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="7b4b9-151">W portalu Azure na **AirWatch** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7b4b9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="7b4b9-155">Na **AirWatch domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="7b4b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-157">a.</span></span> <span data-ttu-id="7b4b9-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="7b4b9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="7b4b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-159">b.</span></span> <span data-ttu-id="7b4b9-160">W **identyfikator** tekstowym, wpisz wartość jako`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="7b4b9-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b4b9-161">Ta wartość nie jest rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-161">This value is not the real.</span></span> <span data-ttu-id="7b4b9-162">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="7b4b9-163">Skontaktuj się z [zespołem pomocy technicznej klienta AirWatch](http://www.air-watch.com/company/contact-us/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="7b4b9-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="7b4b9-166">Na **konfiguracji AirWatch** , kliknij przycisk **skonfigurować AirWatch** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7b4b9-167">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="7b4b9-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-169">Click **Save** button.</span></span>

    <span data-ttu-id="7b4b9-170">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="7b4b9-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="7b4b9-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy AirWatch.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="7b4b9-172">W okienku nawigacji po lewej stronie kliknij **kont**, a następnie kliknij przycisk **Administratorzy**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="7b4b9-173">![Administratorzy](./media/active-directory-saas-airwatch-tutorial/ic791920.png "administratorów")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="7b4b9-174">Rozwiń węzeł **ustawienia** menu, a następnie kliknij przycisk **usług katalogowych**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="7b4b9-175">![Ustawienia](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="7b4b9-176">Kliknij przycisk **użytkownika** karcie **bazowa nazwa Wyróżniająca** tekstowym, wpisz nazwę domeny, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="7b4b9-177">![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791922.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="7b4b9-178">Kliknij przycisk **serwera** kartę.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="7b4b9-179">![Serwer](./media/active-directory-saas-airwatch-tutorial/ic791923.png "serwera")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="7b4b9-180">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="7b4b9-181">![Przekaż](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Przekaż")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="7b4b9-182">a.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-182">a.</span></span> <span data-ttu-id="7b4b9-183">Jako **typ katalogu**, wybierz pozycję **Brak**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="7b4b9-184">b.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-184">b.</span></span> <span data-ttu-id="7b4b9-185">Wybierz **SAML jest używany do uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="7b4b9-186">c.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-186">c.</span></span> <span data-ttu-id="7b4b9-187">Aby przekazać pobranego certyfikatu, kliknij przycisk **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="7b4b9-188">W **żądania** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="7b4b9-189">![Żądanie](./media/active-directory-saas-airwatch-tutorial/ic791925.png "żądania")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="7b4b9-190">a.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-190">a.</span></span> <span data-ttu-id="7b4b9-191">Jako **żądania typu powiązania**, wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="7b4b9-192">b.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-192">b.</span></span> <span data-ttu-id="7b4b9-193">W portalu Azure na **skonfigurować logowanie jednokrotne w Airwatch** strony okna dialogowego, kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **tożsamości pojedynczy znak na adres URL dostawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="7b4b9-194">c.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-194">c.</span></span> <span data-ttu-id="7b4b9-195">Jako **NameID Format**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="7b4b9-196">d.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-196">d.</span></span> <span data-ttu-id="7b4b9-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-197">Click **Save**.</span></span>

14. <span data-ttu-id="7b4b9-198">Kliknij przycisk **użytkownika** karcie ponownie.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="7b4b9-199">![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791926.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="7b4b9-200">W **atrybutu** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="7b4b9-201">![Atrybut](./media/active-directory-saas-airwatch-tutorial/ic791927.png "atrybutu")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="7b4b9-202">a.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-202">a.</span></span> <span data-ttu-id="7b4b9-203">W **identyfikator obiektu** pole tekstowe, typ **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="7b4b9-204">b.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-204">b.</span></span> <span data-ttu-id="7b4b9-205">W **Username** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="7b4b9-206">c.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-206">c.</span></span> <span data-ttu-id="7b4b9-207">W **Nazwa wyświetlana** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="7b4b9-208">d.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-208">d.</span></span> <span data-ttu-id="7b4b9-209">W **imię** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="7b4b9-210">e.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-210">e.</span></span> <span data-ttu-id="7b4b9-211">W **nazwisko** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="7b4b9-212">f.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-212">f.</span></span> <span data-ttu-id="7b4b9-213">W **E-mail** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="7b4b9-214">g.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-214">g.</span></span> <span data-ttu-id="7b4b9-215">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b4b9-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b4b9-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b4b9-217">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7b4b9-219">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b4b9-220">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b4b9-222">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b4b9-224">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b4b9-226">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b4b9-228">a.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-228">a.</span></span> <span data-ttu-id="7b4b9-229">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b4b9-230">b.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-230">b.</span></span> <span data-ttu-id="7b4b9-231">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7b4b9-232">c.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-232">c.</span></span> <span data-ttu-id="7b4b9-233">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b4b9-234">d.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-234">d.</span></span> <span data-ttu-id="7b4b9-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="7b4b9-236">Tworzenie użytkownika testowego AirWatch</span><span class="sxs-lookup"><span data-stu-id="7b4b9-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="7b4b9-237">Aby umożliwić użytkownikom usługi Azure AD zalogować się do AirWatch, ich należy udostępnić w celu AirWatch.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="7b4b9-238">Gdy AirWatch, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="7b4b9-239">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7b4b9-240">Zaloguj się do Twojego **AirWatch** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="7b4b9-241">W okienku nawigacji po lewej stronie kliknij **kont**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="7b4b9-242">![Użytkownicy](./media/active-directory-saas-airwatch-tutorial/ic791929.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="7b4b9-243">W **użytkowników** menu, kliknij przycisk **widok listy**, a następnie kliknij przycisk **Dodaj \> Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="7b4b9-244">![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="7b4b9-245">Na **Dodaj / Edytuj użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7b4b9-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="7b4b9-246">![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="7b4b9-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="7b4b9-247">Typ **Username**, **hasło**, **Potwierdź hasło**, **imię**, **nazwisko**, **adres E-mail** poprawnego konta usługi Azure Active Directory ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="7b4b9-248">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="7b4b9-249">Możesz użyć innych AirWatch użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AirWatch do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b4b9-250">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b4b9-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b4b9-251">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu AirWatch.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7b4b9-253">**Aby przypisać Simona Britta AirWatch, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7b4b9-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="7b4b9-254">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7b4b9-256">Na liście aplikacji zaznacz **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-256">In the applications list, select **AirWatch**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="7b4b9-258">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7b4b9-260">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-260">Click **Add** button.</span></span> <span data-ttu-id="7b4b9-261">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7b4b9-263">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7b4b9-264">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b4b9-265">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b4b9-266">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b4b9-266">Testing single sign-on</span></span>

<span data-ttu-id="7b4b9-267">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7b4b9-268">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="7b4b9-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7b4b9-269">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b4b9-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7b4b9-270">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7b4b9-270">Additional resources</span></span>

* [<span data-ttu-id="7b4b9-271">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b4b9-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b4b9-272">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b4b9-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

