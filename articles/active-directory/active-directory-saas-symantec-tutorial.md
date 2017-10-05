---
title: "Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usług zabezpieczeń firmy Symantec w sieci Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="3d595-103">Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="3d595-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="3d595-104">Z tego samouczka dowiesz się, jak integracji Twoje konto usługi zabezpieczeń firmy Symantec w sieci Web (WSS) przy użyciu konta usługi Azure Active Directory (Azure AD), dzięki czemu WSS można uwierzytelnić użytkownika końcowego udostępniane w usłudze Azure AD przy użyciu uwierzytelniania SAML i wymuszać reguły zasady na poziomie użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="3d595-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="3d595-105">Integrowanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3d595-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d595-106">Zarządzaj wszystkimi użytkowników i grupy używane przez Twoje konto programu WSS w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d595-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="3d595-107">Zezwalaj użytkownikom końcowym uwierzytelnić się programu WSS przy użyciu swoich poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d595-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="3d595-108">Włącz wymuszania użytkowników i grupy poziomu reguł zdefiniowanych w ramach konta programu WSS.</span><span class="sxs-lookup"><span data-stu-id="3d595-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="3d595-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d595-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d595-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d595-110">Prerequisites</span></span>

<span data-ttu-id="3d595-111">Aby skonfigurować integrację usługi Azure AD z sieci Web usług zabezpieczeń (WSS) firmy Symantec, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3d595-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="3d595-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d595-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d595-113">Konto usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="3d595-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="3d595-114">Aby przetestować kroki opisane w tym samouczku, zaleca się przy użyciu konta programu WSS, który jest obecnie używana w celu produkcji.</span><span class="sxs-lookup"><span data-stu-id="3d595-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="3d595-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3d595-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d595-116">Nie należy używać konta programu WSS, który jest obecnie używana w celu produkcji dla tego testu, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3d595-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="3d595-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d595-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d595-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3d595-118">Scenario description</span></span>
<span data-ttu-id="3d595-119">W tym samouczku skonfigurujesz usługi Azure AD, aby włączyć logowanie jednokrotne do programu WSS przy użyciu poświadczeń użytkownika zdefiniowane w ramach konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d595-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="3d595-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3d595-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d595-121">Dodawanie aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii</span><span class="sxs-lookup"><span data-stu-id="3d595-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="3d595-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3d595-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="3d595-123">Dodawanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii</span><span class="sxs-lookup"><span data-stu-id="3d595-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="3d595-124">Aby skonfigurować integrację usługi zabezpieczeń firmy Symantec w sieci Web (WSS) do usługi Azure AD, należy dodać usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3d595-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d595-125">**Aby dodać usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3d595-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d595-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3d595-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="3d595-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3d595-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d595-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3d595-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="3d595-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3d595-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="3d595-133">W polu wyszukiwania wpisz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**, wybierz pozycję **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="3d595-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web zabezpieczeń usługi (WSS) na liście wyników](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d595-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3d595-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3d595-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="3d595-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d595-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem w sieci Web usług zabezpieczeń (WSS) firmy Symantec jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d595-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="3d595-138">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i powiązanych użytkowników w sieci Web usług zabezpieczeń (WSS) firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="3d595-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="3d595-139">W firmy Symantec w sieci Web zabezpieczeń usługi (WSS), przypisz wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="3d595-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d595-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="3d595-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d595-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3d595-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d595-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3d595-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d595-143">**[Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  — aby odpowiednikiem Simona Britta w firmy Symantec w sieci Web usługi zabezpieczeń (WSS) połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3d595-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d595-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3d595-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d595-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="3d595-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3d595-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3d595-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3d595-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="3d595-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="3d595-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3d595-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="3d595-149">W portalu Azure na **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3d595-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="3d595-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="3d595-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="3d595-153">Na **domeny usługi (WSS) zabezpieczeń firmy Symantec w sieci Web i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3d595-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Domena usługi zabezpieczeń firmy Symantec w sieci Web (WSS) i adresy URL pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="3d595-155">a.</span><span class="sxs-lookup"><span data-stu-id="3d595-155">a.</span></span> <span data-ttu-id="3d595-156">W **identyfikator** tekstowym, wpisz adres URL:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="3d595-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="3d595-157">b.</span><span class="sxs-lookup"><span data-stu-id="3d595-157">b.</span></span> <span data-ttu-id="3d595-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="3d595-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d595-159">Skontaktuj się z [zespołem pomocy technicznej klienta usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](https://www.symantec.com/contact-us) Jeśli wartości **identyfikator** i **adres URL odpowiedzi** jakiegoś powodu nie działają.</span><span class="sxs-lookup"><span data-stu-id="3d595-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="3d595-160">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3d595-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="3d595-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d595-162">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d595-164">Aby skonfigurować rejestrację jednokrotną po stronie usługi zabezpieczeń firmy Symantec w sieci Web (WSS), zapoznaj się z dokumentacją online programu WSS.</span><span class="sxs-lookup"><span data-stu-id="3d595-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="3d595-165">Pobrany **XML metadanych** pliku musi być importowane do portalu programu WSS.</span><span class="sxs-lookup"><span data-stu-id="3d595-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="3d595-166">Skontaktuj się z [usługi zabezpieczeń firmy Symantec w sieci Web (WSS) obsługuje zespołu](https://www.symantec.com/contact-us) Jeśli potrzebujesz pomocy z konfiguracją w portalu programu WSS.</span><span class="sxs-lookup"><span data-stu-id="3d595-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="3d595-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="3d595-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d595-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="3d595-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d595-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d595-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d595-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d595-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3d595-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3d595-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="3d595-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3d595-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d595-174">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d595-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3d595-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3d595-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3d595-178">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="3d595-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3d595-180">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3d595-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3d595-182">a.</span><span class="sxs-lookup"><span data-stu-id="3d595-182">a.</span></span> <span data-ttu-id="3d595-183">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d595-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d595-184">b.</span><span class="sxs-lookup"><span data-stu-id="3d595-184">b.</span></span> <span data-ttu-id="3d595-185">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3d595-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3d595-186">c.</span><span class="sxs-lookup"><span data-stu-id="3d595-186">c.</span></span> <span data-ttu-id="3d595-187">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="3d595-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3d595-188">d.</span><span class="sxs-lookup"><span data-stu-id="3d595-188">d.</span></span> <span data-ttu-id="3d595-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3d595-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="3d595-190">Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="3d595-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="3d595-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w sieci Web usług zabezpieczeń (WSS) firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="3d595-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="3d595-192">Odpowiednie nazwy użytkownika końcowego mogą być utworzone ręcznie w portalu programu WSS lub poczekać dla użytkowników/grupy udostępniane w usłudze Azure AD do synchronizacji programu WSS portalu po kilku minutach (~ 15 minut).</span><span class="sxs-lookup"><span data-stu-id="3d595-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="3d595-193">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3d595-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="3d595-194">Publiczny adres IP komputera użytkownika końcowego, która będzie używana do przeglądania witryny sieci Web muszą być udostępniane w portalu usługi zabezpieczeń firmy Symantec w sieci Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="3d595-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3d595-195">Sprawdź [kliknij tutaj](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) uzyskać komputera na publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="3d595-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3d595-196">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d595-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="3d595-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do sieci Web usług zabezpieczeń (WSS) firmy Symantec.</span><span class="sxs-lookup"><span data-stu-id="3d595-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="3d595-199">**Aby przypisać Simona Britta do usługi zabezpieczeń firmy Symantec w sieci Web (WSS), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3d595-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="3d595-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3d595-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3d595-202">Na liście aplikacji zaznacz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="3d595-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Łącze usługi zabezpieczeń firmy Symantec w sieci Web (WSS) na liście aplikacji](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="3d595-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3d595-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="3d595-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d595-206">Click **Add** button.</span></span> <span data-ttu-id="3d595-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3d595-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="3d595-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3d595-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d595-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3d595-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d595-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3d595-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3d595-212">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3d595-212">Test single sign-on</span></span>

<span data-ttu-id="3d595-213">W tej sekcji przetestujesz funkcji pojedynczego logowania jednokrotnego teraz, gdy skonfigurowano konto programu WSS do użycia usługi Azure AD na potrzeby uwierzytelniania SAML.</span><span class="sxs-lookup"><span data-stu-id="3d595-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="3d595-214">Po skonfigurowaniu serwera proxy ruchu programu WSS, przeglądarki sieci web po otwarciu przeglądarki sieci web i spróbuj przejść do lokacji, a następnie użytkownik zostanie przekierowany do strony logowania systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="3d595-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="3d595-215">Wprowadź poświadczenia użytkownika testowego, że zainicjowano w usłudze Azure AD (czyli BrittaSimon) oraz skojarzone hasło.</span><span class="sxs-lookup"><span data-stu-id="3d595-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="3d595-216">Po uwierzytelnieniu będzie mógł przejść do witryny sieci Web, który został wybrany.</span><span class="sxs-lookup"><span data-stu-id="3d595-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="3d595-217">Należy utworzyć reguły na stronie programu WSS Aby zablokować BrittaSimon przeglądanie do określonej lokacji, a następnie powinna zostać wyświetlona strona bloku WSS przy próbie przejdź do tej lokacji jako użytkownik BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d595-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d595-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3d595-218">Additional resources</span></span>

* [<span data-ttu-id="3d595-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d595-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d595-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d595-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

