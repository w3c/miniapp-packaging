# [Self-Review Questionnaire: Security and Privacy](https://w3ctag.github.io/security-questionnaire/)

## 01. What information might this feature expose to Websites or other parties, and for what purposes is that exposure necessary?

This specification defines the structure of a MiniApp container and how its resources are packed within a single file that MiniApp user agents process. 

It does not require a specific exposition of information publicly. However, a MiniApp package includes features that could describe the target user agent and some characteristics of the necessary running environment, including the version of the operating system and the underlying hardware capabilities (e.g., availability of sensors, type of device, and display capabilities). These platform requirements, specified in the MiniApp manifest, may halt the execution of a MiniApp initialization during the manifest processing phase, revealing some inconsistencies between the app requirements and the user agent's environment. Still, no detailed information about the underlying platform is exposed publicly.

## 02. Do features in your specification expose the minimum amount of information necessary to enable their intended uses?

No information is required to be exposed.

## 03. How do the features in your specification deal with personal information, personally identifiable information (PII), or information derived from them?

MiniApps may deal with personally-identifiable information that can be persisted and preserved in the user agent's sandboxed environment for subsequent app executions. End-users must decide whether to remove all the data stored by the user agent corresponding to one or several MiniApps. _User agents must secure that information_, allowing only instances of the same application to access the data and avoiding the public exposition.       

Users agents should apply mechanisms to minimize these risks.

User agents may, possibly in a manner configured by the user, automatically delete stored data after some time. Users should be able to force the removal of the entire stored data. 

## 04. How do the features in your specification deal with sensitive information?

MiniApps could also deal with sensitive data that the user agent could store. See the point above.

User agents should treat the stored data as potentially sensitive, ensuring that it is adequately deleted from the underlying storage when removing data.

## 05. Do the features in your specification introduce new state for an origin that persists across browsing sessions?

Although the current specification does not describe any mechanism for data persistence across sessions, MiniApps may store data on a user's device retrieved in subsequent sessions. This scenario introduces the risk of user tracking without their knowledge or control. Thus, MiniApp user agents must consider protections to ensure that client-side storage mechanisms cannot be misused to track users without their control. 

## 06. Do the features in your specification expose information about the underlying platform to origins?

The MiniApp Packaging does not specify any concrete mechanism to access and expose information about the underlying platform. However,   MiniApp user agents implement services to handle sensitive information (i.e., operating system, display capabilities, and environmental sensors). Therefore, user agents should define adequate mitigation mechanisms to guarantee that the technical details are not revealed without explicit and meaningful [user consent](https://www.w3.org/TR/design-principles/#consent).

## 07. Does this specification allow an origin to send data to the underlying platform?

Although this document does not specify it, a MiniApp may communicate with the underlying platform through APIs, enabling communication with the hardware and the operating system. User agents should consider the potential risks when implementing the support of these susceptible services. 

## 08. Do features in this specification enable access to device sensors?

Although this document does not specify it, a MiniApp may communicate with the underlying platform through APIs, enabling communication with the hardware and the operating system. User agents should consider the potential risks when implementing the support of these susceptible services. 

## 09. Do features in this specification enable new script execution/loading mechanisms?

This specification defines a new mechanism to pack, distribute and load apps through a concrete configuration ([manifest](https://www.w3.org/TR/miniapp-manifest) file) that specifies the application's entry points and routes. (i.e., the [`pages` member](https://www.w3.org/TR/miniapp-manifest/#pages-member) in the manifest). Since the MiniApp components are included locally in the package, the user agent must check the availability of the resources specified in the manifest and the complementary files included within the container (i.e., media files, scripts, stylesheets, among others). 

User agents should mitigate the potential vulnerability during the initialization and loading phase by limiting the type of resources to be loaded and implementing a sandboxed environment that blocks access to sensitive services by default.

A MiniApp package may include resources of any type, including malicious scripts. Therefore, MiniApp user agents must strictly limit the resources to be processed, minimizing the attack surface by discarding those not declared in the manifest and properly bound from the components. 

### XSS (Cross-Site Scripting) vulnerabilities 

MiniApp user agents are vulnerable to XSS attacks, concretely getting and processing external resources like images, data sources, and scripts. Therefore, user agents should limit the attack vectors and mitigate the risks by implementing a Content Security Policy (CSP) to control the resources that a MiniApp can fetch or execute. (Under discussion in #42.)

## 10. Do features in this specification allow an origin to access other devices?

Not explicitly in this specification, but MiniApps may access other services using APIs. MiniApp user agents must consider each case, preserving privacy and security.  

## 11. Do features in this specification allow an origin some measure of control over a user agent's native UI?

No. User agents may install apps on the underlying platform (through home-screen shortcuts, icons on the desktop, and similar) in a transparent and reversible process. Still, it does not include features to modify the user agent's native UI.  

## 12. What temporary identifiers do the features in this specification create or expose to the web?

N/A.

## 13. How does this specification distinguish between behavior in first-party and third-party contexts?

This specification considers only the resources contained in a MiniApp package. MiniApp user agents should consider the specific risks of implementing APIs that enable using third-party resources.

## 14. How do the features in this specification work in the context of a browser's  Private Browsing or Incognito mode?

So far, the specification only considers a normal state.

## 15. Does this specification have both "Security Considerations" and "Privacy Considerations" sections?

Yes. [Security](https://www.w3.org/TR/miniapp-packaging/#sec-security), and [Privacy](https://www.w3.org/TR/miniapp-packaging/#sec-privacy) sections.

## 16. Do features in your specification enable origins to downgrade default security protections?

No

## 17. How does your feature handle non- "fully active" documents?

N/A

## 18. What should this questionnaire have asked?

...