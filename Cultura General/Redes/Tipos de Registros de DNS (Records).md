
|Tipo|Significado|Descripción|Ejemplo|
|---|---|---|---|
|**A**|Address|Traduce **Nombre → IPv4**. Es el estándar.|`api.web.com` → `54.21.10.1`|
|**AAAA**|Quad A|Traduce **Nombre → IPv6**.|`api.web.com` → `2001:db8::1`|
|**CNAME**|Canonical Name|Traduce **Nombre → Otro Nombre**. <br><br>  <br><br>⚠️ _No sirve para el dominio raíz (Apex)._|`m.web.com` → `mobile.web.com`|
|**MX**|Mail Exchange|Servidores de **correo**. Prioridad numérica.|`web.com` → `smtp.gmail.com`|
|**NS**|Name Server|Indica los servidores **autorizados** (DNS) de tu zona.|`web.com` → `ns-1.awsdns.com`|
|**TXT**|Text|Texto libre. Se usa para verificar propiedad de dominio o seguridad de email (SPF/DKIM).|"google-site-verification=..."|
|**ALIAS**|**AWS Exclusive**|Como un CNAME, pero **sí permite usarse en la raíz**. Apunta a recursos AWS (ELB, CloudFront, S3) gratis y dinámicamente.|`web.com` → `my-loadbalancer.amazonaws.com`|
