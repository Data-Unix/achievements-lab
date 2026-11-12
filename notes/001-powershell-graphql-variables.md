# Pasar texto a GraphQL con gh desde PowerShell sin romper comillas

Windows PowerShell 5.1 elimina las comillas dobles incrustadas al pasar argumentos a ejecutables nativos como `gh.exe`. Una query con `title:"Hola mundo"` llega rota y aparecen errores como `Expected COLON` o `accepts 1 arg(s), received N`.

Solución: no meter literales dentro de la query y pasarlos como variables GraphQL.

```powershell
gh api graphql -f query='mutation($t:String!){ ... title:$t ... }' -f t='Hola mundo'
```

- La query no contiene ninguna comilla doble.
- Cada valor va con `-f clave='valor'` (comillas simples de PowerShell).
- PowerShell 7.3+ mejoró el paso de argumentos a nativos (`$PSNativeCommandArgumentPassing`), pero las variables funcionan en cualquier versión.
