```mermaid
sequenceDiagram
    participant User
    participant ArgoCD_CLI as ArgoCD (CLI)
    participant Browser as Web Browser
    participant Keycloak as Keycloak (Authorization Server)

    Note over User: Starts CLI Login (Client Auth)

    User->>ArgoCD_CLI: Run `argocd login`
    ArgoCD_CLI->>Browser: Open Keycloak login page<br/> (http://localhost:8085/auth/callback)
    Browser->>Keycloak: User enters credentials
    Keycloak->>Browser: Redirect back to CLI
    Browser->>ArgoCD_CLI: Authorization Code (http://localhost:8085/auth/callback)
    ArgoCD_CLI->>Keycloak: ❌ **Fails - Missing Client Secret**
    
    Note over User: Login fails! ❌ <br/> ArgoCD CLI does not support client authentication.

```
