---
title: "Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usług sieci Web firmy Amazon (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="fbc97-103">Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS)</span><span class="sxs-lookup"><span data-stu-id="fbc97-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="fbc97-104">Z tego samouczka dowiesz się integrowanie Amazon Web Services (AWS) z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbc97-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbc97-105">Integrowanie usługi Amazon Web Services (AWS) z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fbc97-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbc97-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usług sieci Web firmy Amazon (AWS)</span><span class="sxs-lookup"><span data-stu-id="fbc97-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="fbc97-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Amazon Web Services (AWS) (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc97-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbc97-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fbc97-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbc97-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbc97-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="fbc97-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fbc97-110">Prerequisites</span></span>

<span data-ttu-id="fbc97-111">Aby skonfigurować integrację usługi Azure AD z Amazon Web Services (AWS), potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fbc97-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="fbc97-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbc97-113">Amazon Web Services (AWS) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fbc97-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbc97-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbc97-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fbc97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbc97-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fbc97-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fbc97-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbc97-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbc97-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fbc97-118">Scenario description</span></span>
<span data-ttu-id="fbc97-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fbc97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbc97-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fbc97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbc97-121">Dodawanie Amazon Web Services (AWS) z galerii</span><span class="sxs-lookup"><span data-stu-id="fbc97-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="fbc97-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fbc97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="fbc97-123">Dodawanie Amazon Web Services (AWS) z galerii</span><span class="sxs-lookup"><span data-stu-id="fbc97-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="fbc97-124">Aby skonfigurować integrację z usługami sieci Web Amazon (AWS) do usługi Azure AD, należy dodać Amazon Web Services (AWS) z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fbc97-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbc97-125">**Aby dodać Amazon Web Services (AWS) z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fbc97-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbc97-126">W  **[Azure Portal](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fbc97-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="fbc97-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbc97-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="fbc97-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="fbc97-133">W polu wyszukiwania wpisz **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="fbc97-135">W panelu wyników wybierz **Amazon Web Services (AWS)**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fbc97-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbc97-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fbc97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbc97-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Amazon Web usługi (AWS) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbc97-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Amazon Web Services (AWS) jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc97-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="fbc97-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="fbc97-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="fbc97-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Amazon Web Services (AWS), należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="fbc97-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbc97-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fbc97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbc97-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fbc97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbc97-145">**[Tworzenie użytkownika testowego usług Amazon Web Services](#creating-an-amazon-web-services-test-user)**  — aby mieć odpowiednikiem Simona Britta w Amazon usług sieci Web (AWS) połączonej z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc97-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fbc97-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fbc97-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbc97-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="fbc97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbc97-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fbc97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbc97-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji usługi sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="fbc97-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Amazon Web Services (AWS), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fbc97-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="fbc97-151">W portalu Azure na **Amazon Web Services (AWS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="fbc97-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="fbc97-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="fbc97-155">Na **Amazon Web Services (AWS) domeny i adres URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc97-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="fbc97-157">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fbc97-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="fbc97-159">Aplikacji Amazon Web Services (AWS) oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="fbc97-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="fbc97-160">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbc97-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="fbc97-161">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbc97-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="fbc97-162">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-162">The following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="fbc97-164">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="fbc97-165">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="fbc97-165">Attribute Name</span></span>  | <span data-ttu-id="fbc97-166">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="fbc97-166">Attribute Value</span></span> | <span data-ttu-id="fbc97-167">przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="fbc97-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="fbc97-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="fbc97-168">RoleSessionName</span></span> | <span data-ttu-id="fbc97-169">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="fbc97-169">user.userprincipalname</span></span> | <span data-ttu-id="fbc97-170">https://awS.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="fbc97-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="fbc97-171">Rola</span><span class="sxs-lookup"><span data-stu-id="fbc97-171">Role</span></span>            | <span data-ttu-id="fbc97-172">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="fbc97-172">user.assignedroles</span></span> |  <span data-ttu-id="fbc97-173">https://awS.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="fbc97-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="fbc97-174">Należy skonfigurować Inicjowanie obsługi użytkowników w usłudze Azure AD można pobrać za pomocą konsoli usług AWS wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="fbc97-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="fbc97-175">Przeczytaj poniższe kroki inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="fbc97-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="fbc97-176">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-176">a.</span></span> <span data-ttu-id="fbc97-177">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="fbc97-179">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-179">b.</span></span> <span data-ttu-id="fbc97-180">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="fbc97-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="fbc97-182">c.</span><span class="sxs-lookup"><span data-stu-id="fbc97-182">c.</span></span> <span data-ttu-id="fbc97-183">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="fbc97-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="fbc97-184">Dodaj wartość Namespace podane powyżej.</span><span class="sxs-lookup"><span data-stu-id="fbc97-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="fbc97-185">d.</span><span class="sxs-lookup"><span data-stu-id="fbc97-185">d.</span></span> <span data-ttu-id="fbc97-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-186">Click **Ok**.</span></span>

7. <span data-ttu-id="fbc97-187">Kliknij przycisk **zapisać** przycisk, aby zapisać ustawienia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc97-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fbc97-189">W oknie innej przeglądarki logowania do witryny firmy Amazon Web Services (AWS) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fbc97-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="fbc97-190">Kliknij przycisk **konsoli głównej**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-190">Click **Console Home**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

10. <span data-ttu-id="fbc97-192">Kliknij przycisk **IAM** z **zabezpieczeń, tożsamości i zgodności** usługi.</span><span class="sxs-lookup"><span data-stu-id="fbc97-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][12]

11. <span data-ttu-id="fbc97-194">Kliknij przycisk **dostawców tożsamości**, a następnie kliknij przycisk **Tworzenie dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][13]

12. <span data-ttu-id="fbc97-196">Na **Konfigurowanie dostawcy** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][14]
 
    <span data-ttu-id="fbc97-198">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-198">a.</span></span> <span data-ttu-id="fbc97-199">Jako **typ dostawcy**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="fbc97-200">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-200">b.</span></span> <span data-ttu-id="fbc97-201">W **Nazwa dostawcy** tekstowym, wpisz nazwę dostawcy (np.: *drewna*).</span><span class="sxs-lookup"><span data-stu-id="fbc97-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="fbc97-202">c.</span><span class="sxs-lookup"><span data-stu-id="fbc97-202">c.</span></span> <span data-ttu-id="fbc97-203">Aby przekazać plik metadanych pobranych, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="fbc97-204">d.</span><span class="sxs-lookup"><span data-stu-id="fbc97-204">d.</span></span> <span data-ttu-id="fbc97-205">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="fbc97-206">Na **Sprawdź informacje o dostawcy** strony okna dialogowego, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][15]

14. <span data-ttu-id="fbc97-208">Kliknij przycisk **ról**, a następnie kliknij przycisk **Utwórz nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][16]

15. <span data-ttu-id="fbc97-210">Na **Ustaw nazwę roli** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][17] 

    <span data-ttu-id="fbc97-212">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-212">a.</span></span> <span data-ttu-id="fbc97-213">W **nazwy roli** tekstowym, wpisz nazwę roli (np.: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="fbc97-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="fbc97-214">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-214">b.</span></span> <span data-ttu-id="fbc97-215">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="fbc97-216">Na **wybierz typ roli** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej][18] 

    <span data-ttu-id="fbc97-218">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-218">a.</span></span> <span data-ttu-id="fbc97-219">Wybierz **roli dostęp dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="fbc97-220">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-220">b.</span></span> <span data-ttu-id="fbc97-221">W **Grant sieci Web rejestracji jednokrotnej (WebSSO) dostępu do dostawcy SAML** kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="fbc97-222">Na **ustanowić zaufanie** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej][19] 

    <span data-ttu-id="fbc97-224">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-224">a.</span></span> <span data-ttu-id="fbc97-225">Jako dostawca SAML, należy wybrać dostawcę SAML utworzonym wcześniej (np.: *drewna*)</span><span class="sxs-lookup"><span data-stu-id="fbc97-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="fbc97-226">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-226">b.</span></span> <span data-ttu-id="fbc97-227">Kliknij przycisk **następny krok**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="fbc97-228">Na **Sprawdź zaufania roli** okna dialogowego, kliknij przycisk **następnego kroku**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][32]

19. <span data-ttu-id="fbc97-230">Na **Dołącz zasady** okna dialogowego, kliknij przycisk **następnego kroku**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][33]

20. <span data-ttu-id="fbc97-232">Na **przeglądu** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][34]
 
    <span data-ttu-id="fbc97-234">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-234">a.</span></span> <span data-ttu-id="fbc97-235">Kliknij przycisk **utworzyć rolę**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-235">Click **Create Role**.</span></span>

    <span data-ttu-id="fbc97-236">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-236">b.</span></span> <span data-ttu-id="fbc97-237">Tworzenie ról tyle zgodnie z potrzebami i zamapowania ich na dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fbc97-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="fbc97-238">Teraz skonfigurować przypisywania do pobierania z usług AWS wszystkie role użytkowników</span><span class="sxs-lookup"><span data-stu-id="fbc97-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="fbc97-239">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-239">a.</span></span> <span data-ttu-id="fbc97-240">W konsoli usług AWS logowanie przy użyciu konta głównego</span><span class="sxs-lookup"><span data-stu-id="fbc97-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="fbc97-241">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-241">b.</span></span> <span data-ttu-id="fbc97-242">W prawym górnym rogu kliknij swoją nazwę, a następnie kliknij przycisk **moje poświadczenia zabezpieczeń** opcji.</span><span class="sxs-lookup"><span data-stu-id="fbc97-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="fbc97-243">Spowoduje to otwarcie ekranu jako komunikat ostrzegawczy.</span><span class="sxs-lookup"><span data-stu-id="fbc97-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="fbc97-244">Kliknij przycisk **poświadczenia zabezpieczeń** przycisk, aby przekazać ekranu.</span><span class="sxs-lookup"><span data-stu-id="fbc97-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][36]

       ![Konfigurowanie rejestracji jednokrotnej][37]

    <span data-ttu-id="fbc97-247">c.</span><span class="sxs-lookup"><span data-stu-id="fbc97-247">c.</span></span> <span data-ttu-id="fbc97-248">W sekcji klucze dostępu kliknij **Utwórz nowy klucz dostępu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fbc97-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="fbc97-249">Spowoduje to wygenerowanie Identyfikatora klucza dostępu i wartość tokenu.</span><span class="sxs-lookup"><span data-stu-id="fbc97-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Konfigurowanie rejestracji jednokrotnej][38]

    <span data-ttu-id="fbc97-251">d.</span><span class="sxs-lookup"><span data-stu-id="fbc97-251">d.</span></span> <span data-ttu-id="fbc97-252">Skopiuj obie te wartości i go również pobrać, tak aby nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="fbc97-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="fbc97-253">e.</span><span class="sxs-lookup"><span data-stu-id="fbc97-253">e.</span></span> <span data-ttu-id="fbc97-254">W portalu Azure na stronie integracji aplikacji Amazon Web Services (AWS) kliknij **inicjowania obsługi administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][35]

    <span data-ttu-id="fbc97-256">f.</span><span class="sxs-lookup"><span data-stu-id="fbc97-256">f.</span></span> <span data-ttu-id="fbc97-257">Ustaw tryb inicjowania obsługi administracyjnej **automatyczne**</span><span class="sxs-lookup"><span data-stu-id="fbc97-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Konfigurowanie rejestracji jednokrotnej][39]

    <span data-ttu-id="fbc97-259">g.</span><span class="sxs-lookup"><span data-stu-id="fbc97-259">g.</span></span> <span data-ttu-id="fbc97-260">Teraz w **clientsecret** i **klucz tajny tokenu** Wklej odpowiednie wartości, które zostały skopiowane z konsoli usług AWS.</span><span class="sxs-lookup"><span data-stu-id="fbc97-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="fbc97-261">h.</span><span class="sxs-lookup"><span data-stu-id="fbc97-261">h.</span></span> <span data-ttu-id="fbc97-262">Możesz kliknąć **Testuj połączenie** przycisk, aby przetestować połączenie.</span><span class="sxs-lookup"><span data-stu-id="fbc97-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="fbc97-263">Gdy zostanie pomyślnie przesłany można uruchomić łącznik inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="fbc97-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Konfigurowanie rejestracji jednokrotnej][40]

    <span data-ttu-id="fbc97-265">i.</span><span class="sxs-lookup"><span data-stu-id="fbc97-265">i.</span></span> <span data-ttu-id="fbc97-266">Teraz włączyć stan inicjowania obsługi administracyjnej **na**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="fbc97-267">Spowoduje to uruchomienie pobierania ról z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbc97-267">This starts fetching the roles from the application.</span></span>

       ![Konfigurowanie rejestracji jednokrotnej][41]

    > [!NOTE]
    > <span data-ttu-id="fbc97-269">Azure działa Usługa AD inicjowania obsługi administracyjnej co po pewnym czasie, aby zsynchronizować role z usług AWS.</span><span class="sxs-lookup"><span data-stu-id="fbc97-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="fbc97-270">Powinna zostać wyświetlona dostawcy tożsamości dołączony ról usług AWS z usługą Azure AD i można ich użyć podczas przypisywania aplikacji do użytkowników lub grup.</span><span class="sxs-lookup"><span data-stu-id="fbc97-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbc97-271">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc97-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbc97-272">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fbc97-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="fbc97-274">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fbc97-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbc97-275">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fbc97-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbc97-277">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fbc97-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbc97-279">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbc97-281">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbc97-283">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-283">a.</span></span> <span data-ttu-id="fbc97-284">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbc97-285">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-285">b.</span></span> <span data-ttu-id="fbc97-286">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbc97-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbc97-287">c.</span><span class="sxs-lookup"><span data-stu-id="fbc97-287">c.</span></span> <span data-ttu-id="fbc97-288">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbc97-289">d.</span><span class="sxs-lookup"><span data-stu-id="fbc97-289">d.</span></span> <span data-ttu-id="fbc97-290">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="fbc97-291">Tworzenie użytkownika testowego usług Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="fbc97-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="fbc97-292">Aby włączyć użytkowników usługi Azure AD zalogować się do usługi sieci Web firmy Amazon (AWS), są udostępniane do usług sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="fbc97-293">W przypadku Amazon Web Services (usług AWS), inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="fbc97-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="fbc97-294">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fbc97-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fbc97-295">Zaloguj się do Twojego **Amazon Web Services (AWS)** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fbc97-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="fbc97-296">Kliknij przycisk **konsoli głównej** ikony.</span><span class="sxs-lookup"><span data-stu-id="fbc97-296">Click the **Console Home** icon.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

3. <span data-ttu-id="fbc97-298">Tożsamość i zarządzanie dostępem.</span><span class="sxs-lookup"><span data-stu-id="fbc97-298">Click Identity and Access Management.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][28]

4. <span data-ttu-id="fbc97-300">Na pulpicie nawigacyjnym kliknij **użytkowników**, a następnie kliknij przycisk **Utwórz nowych użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

5. <span data-ttu-id="fbc97-302">W oknie dialogowym Tworzenie użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fbc97-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][30]   
    
    <span data-ttu-id="fbc97-304">a.</span><span class="sxs-lookup"><span data-stu-id="fbc97-304">a.</span></span> <span data-ttu-id="fbc97-305">W **wprowadź nazwy użytkowników** pól tekstowych, wpisz nazwę użytkownika Simona Brita (userprincipalname) w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc97-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="fbc97-306">b.</span><span class="sxs-lookup"><span data-stu-id="fbc97-306">b.</span></span> <span data-ttu-id="fbc97-307">Kliknij przycisk **utworzyć.**</span><span class="sxs-lookup"><span data-stu-id="fbc97-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbc97-308">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc97-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbc97-309">W tej sekcji można włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udostępnienie jej do usługi sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="fbc97-311">**Aby przypisać Simona Britta do Amazon Web Services (AWS), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fbc97-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="fbc97-312">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fbc97-314">Na liście aplikacji zaznacz **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="fbc97-316">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fbc97-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="fbc97-318">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fbc97-318">Click **Add** button.</span></span> <span data-ttu-id="fbc97-319">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="fbc97-321">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fbc97-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbc97-322">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbc97-323">Na **wybierz rolę** , a następnie wybierz odpowiednią rolę dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fbc97-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="fbc97-324">Te role są wyświetlane z nazwą roli i nazwa dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fbc97-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="fbc97-325">Dzięki temu można łatwo zidentyfikować role z usług AWS.</span><span class="sxs-lookup"><span data-stu-id="fbc97-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="fbc97-326">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fbc97-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbc97-327">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fbc97-327">Testing single sign-on</span></span>

<span data-ttu-id="fbc97-328">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fbc97-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fbc97-329">Po kliknięciu kafelka Amazon Web Services (AWS) w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi sieci Web firmy Amazon (AWS).</span><span class="sxs-lookup"><span data-stu-id="fbc97-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fbc97-330">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fbc97-330">Additional resources</span></span>

* [<span data-ttu-id="fbc97-331">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbc97-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbc97-332">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbc97-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
