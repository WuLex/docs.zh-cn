---
title: '&lt;peerTransport&gt; 的 &lt;transport&gt;'
ms.date: 03/30/2017
ms.assetid: d7116240-845c-4b6f-b203-262de6b597ef
ms.openlocfilehash: aeadf23b4ae6b4b0be18755c43585cbfea418567
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lttransportgt-of-ltpeertransportgt"></a>&lt;peerTransport&gt; 的 &lt;transport&gt;
指定采用此绑定配置的对等方所发送的安全消息的传输类型。  
  
 \<system.serviceModel>  
\<绑定 >  
\<customBinding>  
\<绑定 >  
\<t >  
\<安全 >  
\<transport>  
  
## <a name="syntax"></a>语法  
  
```xml  
<security>  
   <transport credentialType="Certificate/Password" />  
</security>         
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|credentialType|可选。 指定用于验证通过对等传输发送的消息的凭据的类型。 此属性的类型为 <xref:System.ServiceModel.PeerTransportCredentialType>。|  
  
## <a name="credentialtype-attribute"></a>credentialType 属性  
  
|值|描述|  
|-----------|-----------------|  
|证书|对等通道传输的身份验证需要 X509 证书。|  
|密码|对等通道传输的身份验证需要正确的密码。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)|定义对等传输的安全设置。|  
  
## <a name="remarks"></a>备注  
 仅当设置此元素的 mode 属性[\<安全 >](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)设置为`Transport`或`TransportWithMessageCredential`。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement>  
 <xref:System.ServiceModel.PeerSecuritySettings.Transport%2A>  
 <xref:System.ServiceModel.PeerTransportSecuritySettings>  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 [传输安全性](../../../../../docs/framework/wcf/feature-details/transport-security.md)  
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)  
 [选择传输](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)  
 [绑定](../../../../../docs/framework/wcf/bindings.md)  
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
