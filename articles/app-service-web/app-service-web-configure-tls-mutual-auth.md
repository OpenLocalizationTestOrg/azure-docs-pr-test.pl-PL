---
title: tooConfigure aaaHow TLS wzajemnego uwierzytelniania dla aplikacji sieci Web
description: "Dowiedz się, jak tooconfigure klienta toouse aplikacji sieci web certyfikatów uwierzytelniania na TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>Jak tooConfigure TLS wzajemnego uwierzytelniania dla aplikacji sieci Web
## <a name="overview"></a>Omówienie
Przez włączenie różnych typów uwierzytelniania dla niego, można ograniczyć dostęp tooyour aplikacji sieci web Azure. Jednym ze sposobów toodo jest więc tooauthenticate za pomocą certyfikatu klienta, gdy Żądanie hello jest protokołu TLS/SSL. Mechanizm ten nosi nazwę wzajemnego uwierzytelniania protokołu TLS lub uwierzytelnianie certyfikatu klienta i ten artykuł zawiera szczegółowe jak toosetup uwierzytelnianie certyfikatu klienta toouse aplikacji sieci web.

> **Uwaga:** Jeśli uzyskujesz dostęp do witryny za pośrednictwem protokołu HTTP i HTTPS nie, nie otrzymasz żadnych certyfikatu klienta. Dlatego jeśli aplikacja wymaga certyfikatów klienta nie należy zezwalać żądań tooyour aplikacji za pośrednictwem protokołu HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Konfigurowanie aplikacji sieci Web uwierzytelniania certyfikatu klienta
toosetup użytkownika sieci web aplikacji toorequire certyfikatów klientów należy tooadd hello lokacji clientCertEnabled ustawienie dla aplikacji sieci web i ustaw dla niej tootrue. To ustawienie nie jest obecnie dostępna za pośrednictwem hello możliwości zarządzania w hello portalu, a hello interfejsu API REST będzie on potrzebny tooaccomplish toobe używane.

Można użyć hello [narzędzie ARMClient](https://github.com/projectkudu/ARMClient) toomake go łatwo toocraft hello wywołaniu interfejsu API REST. Po zalogowaniu się przy użyciu narzędzia hello należy hello tooissue następujące polecenie:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

zastępowanie wszystko {} informacje dotyczące aplikacji sieci web i utworzeniu pliku o nazwie enableclientcert.json z powitania po JSON zawartości:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Upewnij się, że wartość hello toochange toowherever "Lokalizacja", to aplikacja sieci web znajdujących się np. dla północno-środkowe stany lub zachodnie stany USA itp.

Można również użyć https://resources.azure.com tooflip hello `clientCertEnabled` właściwości zbyt`true`.

> **Uwaga:** uruchamiane ARMClient programu Powershell, należy hello tooescape @ symbol dla pliku JSON hello z tyłu znaczników ".
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>Uzyskiwanie dostępu do powitania klienta certyfikatu z Twojej aplikacji sieci Web
Jeśli używasz programu ASP.NET i skonfigurować uwierzytelnianie certyfikatu klienta toouse aplikacji, certyfikat hello będą dostępne za pośrednictwem hello **HttpRequest.ClientCertificate** właściwości. Dla innych stosy aplikacji hello certyfikatu klienta będą dostępne w Twojej aplikacji za pomocą wartości kodowany w standardzie base64 w nagłówku żądania "X-ARR ClientCert" hello. Aplikacji można utworzyć certyfikat z tej wartości, a następnie użyć go do celów uwierzytelniania i autoryzacji w aplikacji.

## <a name="special-considerations-for-certificate-validation"></a>Uwagi dotyczące weryfikacji certyfikatów
Hello certyfikat klienta, który jest wysyłany toohello aplikacji nie przechodzi przez wszystkie weryfikacji przez platformę Azure Web Apps hello. Sprawdzanie poprawności tego certyfikatu jest odpowiedzialny za hello hello aplikacji sieci web. Oto przykładowy kod platformy ASP.NET, która weryfikuje właściwości certyfikatu na potrzeby uwierzytelniania.

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
