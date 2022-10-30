load('ext://helm_resource', 'helm_resource', 'helm_repo')

# Set up ArgoCD
helm_repo('argo-repo', 'https://argoproj.github.io/argo-helm')
helm_resource(
    'argo-resource', 
    'argo-repo/argo-cd',
    namespace="argocd",
    flags=[
        "--create-namespace",
        "--set-string",
        "configs.secret.argocdServerAdminPassword=$2a$10$0VP4lNi1mvHxjnOLLTs4d.8.UEidGlYSQut5m0DP26A4u0/J6OqS.", # "password"
        "--set-string",
        "configs.secret.argocdServerAdminPasswordMtime=2020-09-01T10:11:12Z",
        "--set-string",
        "server.rbacConfig.policy\\.default=role:readonly",
        "--set-string",
        "server.config.users\\.anonymous\\.enabled=true",
        "--set",
        "configs.params.server\\.insecure=true"
    ],
    port_forwards=["8080:8080"]
)

# Install this chart
helm_resource(
    "applications",
    ".",
    namespace="argocd",
    resource_deps=["argo-resource"]
)