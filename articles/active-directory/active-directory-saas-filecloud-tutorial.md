---
title: 'Samouczek: Integracji Azure Active Directory z FileCloud | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="1aea3-103">Samouczek: Integracji Azure Active Directory z FileCloud</span><span class="sxs-lookup"><span data-stu-id="1aea3-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="1aea3-104">Z tego samouczka dowiesz się integrowanie FileCloud z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1aea3-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1aea3-105">Integracja z usługą Azure AD FileCloud zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1aea3-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1aea3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do FileCloud.</span><span class="sxs-lookup"><span data-stu-id="1aea3-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="1aea3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do FileCloud (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aea3-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1aea3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1aea3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1aea3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1aea3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aea3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1aea3-110">Prerequisites</span></span>

<span data-ttu-id="1aea3-111">Aby skonfigurować integrację usługi Azure AD z FileCloud, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1aea3-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="1aea3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aea3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1aea3-113">FileCloud logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1aea3-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1aea3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1aea3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1aea3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1aea3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1aea3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1aea3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1aea3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1aea3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1aea3-118">Scenario description</span></span>
<span data-ttu-id="1aea3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1aea3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1aea3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1aea3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1aea3-121">Dodawanie FileCloud z galerii</span><span class="sxs-lookup"><span data-stu-id="1aea3-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="1aea3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1aea3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="1aea3-123">Dodawanie FileCloud z galerii</span><span class="sxs-lookup"><span data-stu-id="1aea3-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="1aea3-124">Aby skonfigurować integrację usługi Azure AD FileCloud, należy dodać FileCloud z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1aea3-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1aea3-125">**Aby dodać FileCloud z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1aea3-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1aea3-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1aea3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="1aea3-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1aea3-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="1aea3-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="1aea3-133">W polu wyszukiwania wpisz **FileCloud**, wybierz pozycję **FileCloud** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1aea3-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud na liście wyników](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1aea3-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1aea3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1aea3-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FileCloud w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1aea3-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w FileCloud jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aea3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="1aea3-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w FileCloud musi się.</span><span class="sxs-lookup"><span data-stu-id="1aea3-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="1aea3-139">W FileCloud, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1aea3-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1aea3-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FileCloud, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1aea3-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1aea3-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1aea3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1aea3-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1aea3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1aea3-143">**[Tworzenie użytkownika testowego FileCloud](#create-a-filecloud-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta FileCloud połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1aea3-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1aea3-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1aea3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1aea3-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1aea3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1aea3-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1aea3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1aea3-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji FileCloud.</span><span class="sxs-lookup"><span data-stu-id="1aea3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="1aea3-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z FileCloud, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1aea3-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1aea3-149">W portalu Azure na **FileCloud** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="1aea3-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1aea3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="1aea3-153">Na **FileCloud domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1aea3-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny FileCloud pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="1aea3-155">a.</span><span class="sxs-lookup"><span data-stu-id="1aea3-155">a.</span></span> <span data-ttu-id="1aea3-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="1aea3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="1aea3-157">b.</span><span class="sxs-lookup"><span data-stu-id="1aea3-157">b.</span></span> <span data-ttu-id="1aea3-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="1aea3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1aea3-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1aea3-159">These values are not real.</span></span> <span data-ttu-id="1aea3-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="1aea3-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1aea3-161">Skontaktuj się z [zespołem pomocy technicznej klienta FileCloud](mailto:support@codelathe.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="1aea3-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="1aea3-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1aea3-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="1aea3-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1aea3-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1aea3-166">Na **konfiguracji FileCloud** , kliknij przycisk **skonfigurować FileCloud** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="1aea3-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1aea3-167">Kopiuj **identyfikator jednostki SAML** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="1aea3-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Konfiguracja FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="1aea3-169">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy FileCloud jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1aea3-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="1aea3-170">W lewym okienku nawigacji, kliknij polecenie **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Strona aplikacji w sekcji Ustawienia](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="1aea3-172">Kliknij przycisk **logowania jednokrotnego** karty w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1aea3-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Jedną stronę logowania jednokrotnego kartę w aplikacji](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="1aea3-174">Wybierz **SAML** jako **domyślny typ logowania jednokrotnego** na **ustawienia pojedynczy znak na rejestracji jednokrotnej (SSO)** panelu.</span><span class="sxs-lookup"><span data-stu-id="1aea3-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Jedną stronę logowania jednokrotnego ustawienia panelu w aplikacji](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="1aea3-176">Wklej **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure do **adres URL punktu końcowego IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Pole tekstowe adresu URL punktu końcowego IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="1aea3-178">Otwórz w Notatniku plik metadanych pobranych, skopiuj zawartość go do Schowka, a następnie wklej go do **IdP metadane** textbox w **ustawienia SAML** panelu.</span><span class="sxs-lookup"><span data-stu-id="1aea3-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Sekcja danych Meta IDP po stronie aplikacji](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="1aea3-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1aea3-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="1aea3-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1aea3-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1aea3-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1aea3-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1aea3-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1aea3-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1aea3-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aea3-184">Create an Azure AD test user</span></span>

<span data-ttu-id="1aea3-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1aea3-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="1aea3-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1aea3-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1aea3-188">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1aea3-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1aea3-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1aea3-192">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1aea3-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1aea3-194">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1aea3-194">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1aea3-196">a.</span><span class="sxs-lookup"><span data-stu-id="1aea3-196">a.</span></span> <span data-ttu-id="1aea3-197">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1aea3-198">b.</span><span class="sxs-lookup"><span data-stu-id="1aea3-198">b.</span></span> <span data-ttu-id="1aea3-199">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1aea3-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1aea3-200">c.</span><span class="sxs-lookup"><span data-stu-id="1aea3-200">c.</span></span> <span data-ttu-id="1aea3-201">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="1aea3-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1aea3-202">d.</span><span class="sxs-lookup"><span data-stu-id="1aea3-202">d.</span></span> <span data-ttu-id="1aea3-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="1aea3-204">Tworzenie użytkownika testowego FileCloud</span><span class="sxs-lookup"><span data-stu-id="1aea3-204">Create a FileCloud test user</span></span>

<span data-ttu-id="1aea3-205">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w FileCloud.</span><span class="sxs-lookup"><span data-stu-id="1aea3-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="1aea3-206">FileCloud obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="1aea3-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1aea3-207">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1aea3-207">There is no action item for you in this section.</span></span> <span data-ttu-id="1aea3-208">Nowy użytkownik został utworzony podczas próby dostępu FileCloud, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1aea3-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1aea3-209">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej klienta FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="1aea3-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1aea3-210">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aea3-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="1aea3-211">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu FileCloud.</span><span class="sxs-lookup"><span data-stu-id="1aea3-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="1aea3-213">**Aby przypisać Simona Britta FileCloud, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1aea3-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1aea3-214">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1aea3-216">Na liście aplikacji zaznacz **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-216">In the applications list, select **FileCloud**.</span></span>

    ![Łącze FileCloud na liście aplikacji](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="1aea3-218">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1aea3-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="1aea3-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1aea3-220">Click **Add** button.</span></span> <span data-ttu-id="1aea3-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="1aea3-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1aea3-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1aea3-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1aea3-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1aea3-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1aea3-226">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1aea3-226">Test single sign-on</span></span>

<span data-ttu-id="1aea3-227">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1aea3-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1aea3-228">Po kliknięciu kafelka FileCloud w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji FileCloud.</span><span class="sxs-lookup"><span data-stu-id="1aea3-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1aea3-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1aea3-229">Additional resources</span></span>

* [<span data-ttu-id="1aea3-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aea3-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1aea3-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1aea3-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

