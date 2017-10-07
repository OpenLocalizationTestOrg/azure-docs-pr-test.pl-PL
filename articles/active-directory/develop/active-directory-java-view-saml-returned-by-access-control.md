---
title: "aaaView zwrócił SAML hello usłudze kontroli dostępu (Java)"
description: "Dowiedz się, jak tooview SAML zwrócony przez hello usłudze kontroli dostępu w aplikacji Java hostowanej na platformie Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Jak tooview SAML zwrócony przez hello usłudze kontroli dostępu platformy Azure
W tym przewodniku opisano sposób hello tooview bazowy Security (Assertion Markup Language SAML) wypychaniu tooyour aplikacji hello Azure usługi kontroli dostępu (ACS). Przewodnik Hello opiera się na powitania [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md) tematu, podając kod, który wyświetla informacje o hello SAML. aplikacji Hello ukończone będzie wyglądać podobnie następujące toohello.

![Przykładowe dane wyjściowe SAML][saml_output]

Aby uzyskać więcej informacji dotyczących usług ACS, zobacz hello [następne kroki](#next_steps) sekcji.

> [!NOTE]
> Hello Azure dostęp do usług formant filtru jest podgląd technologii społeczności. Jako wydaniu wstępnym oprogramowania go nie jest oficjalnie obsługiwana przez firmę Microsoft.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete hello zadania w tym przewodniku, pełną hello próbki w [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md) i używać go jako hello punkt początkowy dla tego samouczka.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Dodaj hello JspWriter biblioteki tooyour kompilacji ścieżkę i wdrożenia zestawu
Dodaj bibliotekę hello, który zawiera hello **javax.servlet.jsp.JspWriter** tooyour klasy kompilacji zestawu ścieżkę i wdrożenia. Jeśli używasz Tomcat Biblioteka hello jest **jsp api.jar**, który znajduje się w hello Apache **lib** folderu.

1. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyACSHelloWorld**, kliknij przycisk **ścieżkę kompilacji**, kliknij przycisk **Konfiguruj ścieżkę kompilacji**, kliknij hello **biblioteki** , a następnie kliknij pozycję **Dodaj zewnętrzne JARs**.
2. W hello **JAR wybór** okno dialogowe, przejdź toohello niezbędne JAR, zaznacz go, a następnie kliknij **Otwórz**.
3. Z hello **właściwości MyACSHelloWorld** nadal otwarty, kliknij przycisk okna dialogowego **wdrożenia zestawu**.
4. W hello **zestawu wdrażania Web** okna dialogowego, kliknij przycisk **Dodaj**.
5. W hello **nowe dyrektywa zestawu** okna dialogowego, kliknij przycisk **wpisy ścieżka kompilacji języka Java** , a następnie kliknij przycisk **dalej**.
6. Wybierz odpowiednią bibliotekę hello i kliknij przycisk **Zakończ**.
7. Kliknij przycisk **OK** tooclose hello **właściwości MyACSHelloWorld** okna dialogowego.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Modyfikowanie toodisplay pliku JSP hello SAML
Modyfikowanie **index.jsp** hello toouse następującego kodu.

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
1. Uruchom aplikację w emulatorze komputera hello lub wdrożyć tooAzure przy użyciu hello czynności opisane w [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Uruchom przeglądarkę i Otwórz aplikację sieci web. Po zalogowaniu aplikacji tooyour zobaczysz informacje SAML, w tym potwierdzenia zabezpieczeń hello udostępniane przez dostawcę tożsamości hello.

## <a name="next-steps"></a>Następne kroki
toofurther poznać funkcje usług ACS i tooexperiment z bardziej zaawansowanych scenariuszy, zobacz [2.0 usługi kontroli dostępu][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
