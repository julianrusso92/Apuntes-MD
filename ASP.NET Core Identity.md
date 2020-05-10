# ASP.NET Core Identity

## Cosas necesarias

Instalar paquete nuget Microsoft.AspNetCore.Identity.EntityFrameworkCore

- So basically, with the `User` class, we extend the `IdentityUser` class with two additional properties. These properties will be added to the database as well.
- While using claims, we populate the Claim object by providing the type and the value properties of the string type (**new Claim(string type, string value)**). But if we have something more complex, we should use a custom property. Additionally, both ways are searchable but the custom properties are a way to go if we search a lot.
- The `AddIdentityCore` method adds the services that are necessary for user-management actions, such as creating users, [hashing passwords](https://code-maze.com/data-protection-aspnet-core/), password validation, etc.
- If your project requires those features and any additional ones like supporting Roles not only Users, supporting external authentication and SingInManager, as our application does, you have to use the `AddIdentity` method.
- **It is important to mention that ASP.NET Core Identity is a different thing from the Identity Server. ASP.NET Core Identity is a user store whilst the Identity Server offers protocol support for Open ID Connect.**
- Authentication is a process of confirming a user’s identity.
- If the user exists and the password matches the hashed password from the database, we create the `ClaimsIdentity` object with two claims inside (Id and UserName).